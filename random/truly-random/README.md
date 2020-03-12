# Truly Random

#### Object / Data Structure

> Objects hide their data behind abstractions & expose functions that operate on that data. Data structure expose their data and have no meaningful functions. - Robert C. Martin

#### Using 3rd Party code / API

Best practice:

* Don't try out / experiment 3rd Party API with our code
* Write some tests to explore / learn and write them in a way that our application would use the 3rd Party API
* Try to keep things that we cannot control \( 3rd Party API \) separate from our own code base

One of good design pattern to use when trying to separate ever changing 3rd party api form our code base is [Adapter Pattern](https://www.tutorialspoint.com/design_pattern/adapter_pattern.htm).

 

