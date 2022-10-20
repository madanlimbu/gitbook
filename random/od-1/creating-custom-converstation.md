# Creating Custom Converstation

1. Define Conversation using YAML & Message Template in AdminUI
2. Define & Register Custom Interpreter & Action
3. Add Conversation to active list to export in code

#### Define Conversation using YAML in Admin UI

Conversations are defined using YAML.[ \[Conversation Description Language\]](https://docs.opendialog.ai/docs/conversation\_markup)

{% code title="Custom_Conversation.yml" %}
```yaml
conversation:
  id: custom_conversation_unique_name
  scenes:
    opening_scene:
      intents:
        - u:
            i: intent.project.custom_intent
            interpreter: interpreter.project.custom_interpreter
            action: action.project.custom_action
            expected_attributes:
              - id: user.name
        - b:
            i: intent.project.CustomResponse
            completes: true
```
{% endcode %}

#### DefinE Response Template for Outgoing Intent using Admin UI

OpenDialog uses custom XML Style mark up language to describe message template. [\[Message Markup\] ](https://docs.opendialog.ai/docs/message\_markup)

{% code title="Custom_Response_Template" %}
```markup
<message disable_text="true">
    <button-message>
        <text>Getting user name attribute from user context :  {user.name}</text>
        <button>
            <text>Custom Button with Callback</text>
            <callback>custom_callback_id</callback>
            <value>age.100</value>
        </button>
    </button-message>
</message>

```
{% endcode %}

#### File Structure convention

```
app/
    Bot/
        Actions/
            CustomAction::class
        Interpreter/
            CustomInterpreter::class
config/
    project_name/
        action_engine.php
        active_conversations.php
        context_engine.php
        interpreter_engine.php
resources/
    conversations/
        custom_conversation
```

#### Registering Attributes

Attributes like `name` & `age` in the above examples needs to be register in `context_engine` in config file to determine what kind of Attribute they are.

{% code title="config/opendialog/context_engine.php" %}
```php
'custom_attributes' => [
        'name' => \OpenDialogAi\Core\Attribute\StringAttribute::class,
        'age' => \OpenDialogAi\Core\Attribute\IntAttribute::class
    ],
```
{% endcode %}

#### Defining Custom Interpreter

We can use default Interpreter provided by core or define our own custom Interpreter to determine `intent` from user the `utterance`/message in the current context.

Create a custom interpreter class in the dir `app/Bot/Interpreter` this should extend  `BaseInterpreter` from `opendialog/core` .

{% code title="app/Bot/Interpreter/CustomInterpreter.php" %}
```php
namespace App\Bot\Interpreter;

use OpenDialogAi\Core\Conversation\Intent;
use OpenDialogAi\Core\Utterances\UtteranceInterface;
use OpenDialogAi\InterpreterEngine\BaseInterpreter;

class CustomInterpreter extends BaseInterpreter
{
   # Interpreter name/id we defined in Conversation YAML.
    protected static $name = 'interpreter.project.custom_interpreter';
    
    /**
     * Interprets an utterance and returns all matching intents in an array
     * @param UtteranceInterface $utterance
     * @return Intent[]
     */
    public function interpret(UtteranceInterface $utterance): array
    {
        if (!is_empty($utterance->getText())) { 
            # After some logic against $utterance, we can create and 
            # return custom intent that we defined in Conversation YAML earlier.   
            $intent = Intent::createIntentWithConfidence('intent.project.intent', 1);
            return [$intent];
        }     
        return [];
    }
}
```
{% endcode %}

After creating the custom interpreter class, we will still need to **register**/activate this Interpreter. This can be done by adding our custom Interpreter to `custom_interpreters` array list in the interpreter engine config file.

{% code title="config/opendialog/interpreter_engine.php" %}
```php
'custom_interpreters' => [
        \App\Bot\Interpreter\CustomInterpreter::class
        ]
```
{% endcode %}

#### Define custom Action

Action are used mostly to do actual work / task during conversation, It usually works with ContextService & return the result which can then be used by ResponseEngine/Response/MessageTemplates.

Create a custom interpreter class in the dir `app/Bot/Actions` this should extend  `BaseAction` from `opendialog/core` .

{% code title="app/Bot/Actions/CustomAction.php" %}
```php
namespace App\Bot\Actions;

use OpenDialogAi\ActionEngine\Actions\ActionInput;
use OpenDialogAi\ActionEngine\Actions\ActionResult;
use OpenDialogAi\ActionEngine\Actions\BaseAction;

class CustomAction extends BaseAction {
    # Custom action name/id same as the one in Conversation YAML.
    protected $performs = 'action.project.custom_action';
    
    # Define what attribute will be returned as result.
    protected $outputsAttributes = ['name'];
    
    # Behind the scene these attributes will retrived from 
    # appropriate context. {'context.attribute_name'}
    # if no context is defined, session context will be 
    # chossen.
    protected $requiredAttributes = ['user.name', 'age'];
    
    /**
     * Performs the action
     * @param ActionInput $actionInput
     * @return ActionResult
     */
    public function perform(ActionInput $actionInput): ActionResult
    {
        $name_attr = $actionInput->attributeBag->getAttribute('name');
        $name = $attr->getValue();
        
        // Do some query or logic actions
        
        $name_attr->setValue('New Name');        
        return ActionResult::createSuccessfulActionResultWithAttributes([$name_attr]);
    }
}
```
{% endcode %}

&#x20;Similar to Custom Interpreter, we also need to register the Custom Actions. We can do this in `action_engine` config file.

{% code title="config/project/action_engine.php" %}
```php
return [
    'custom_actions' => [
        \App\Bot\Actions\ButtonAction::class
    ],
];
```
{% endcode %}

#### Exporting Conversation YAML & Message template from Database to Code

Add the conversation name/id to `active_conversations` config file.

{% code title="config/project/active_conversations.php" %}
```php
return [
    'custom_conversation_unique_name'
];
```
{% endcode %}

Then run `artisan` command to export that conversation.

```bash
# if using lando to run containers
lando artisan conversations:export

# else
 php artisan conversations:export 
```

The exported file will be saved at dir `resources/converations/custom_conversation_unique_name` .

#### Custom callback

We can also use callback id to fire an intent. Example in the message template example above we have given the button callback  to `custom_callback_id` ,  we can map this `id` to a intent in `interpreter_engine` config file so that when we receive `callback_id` we can fire the intent.

{% code title="config/project/interpreter_engine.php" %}
```php
'supported_callbacks' => [
        'custom_callback_id' => 'intent.project.custom_intent'
    ]
```
{% endcode %}

#### Command to setup config files

By default most config files are not available in top project level, we can export them using helpful `artisian` command

```bash
php artisan vendor:publish --tag=opendialog-config
```

#### In short

Text/Utterance -> Interpreter checks if valid -> Fires matching Intent -> if Intent has Action in Conversation -> Call Action::Perform -> Action Return Result Value -> Response/Message Template Use that Result value&#x20;

