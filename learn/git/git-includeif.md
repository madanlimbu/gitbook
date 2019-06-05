# Git IncludeIf

### Problem

Most people use their work laptop and some times work on personal project and forget that the username / email being used to commit on those projects are from global git config \( Most likely work account \). 

It would be too much work to include `.gitconfig` for each of the personal projects and set correct name/email. Luckily, we have git config `includeif` to save our day.

### Solution

We will most likely put our personal project inside a folder `~/personal` . Using `includeif` we can set it so that all the following projects inside that folder includes our personal username/email instead of `global user.name`.

Following is the config we set in global config file `~/.gitconfig`

```text
[includeIf "gitdir:~/personal/"]
        path = ~/personal/.gitconfig_include
```

We can then create our config file `.gitconfig_include` inside `~/personal`. Inside this personal config we can add our personal `user.name` and `user.email` like below: 

```text
[user]
        email = personal@email.com
        name = madan95
```

