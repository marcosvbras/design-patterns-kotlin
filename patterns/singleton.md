# Singleton

#### When should I use it?
This design pattern is used when you want to limit the number of instances of a certain class can be created to just one. 

#### Common implementation

In most of programming languages you need to create either a private constructor and a function that can handle an unique instance creation of the class if it is not created yet.

#### Kotlin implementation

Kotlin has a special and reserved keyword to create singletons called `object`:

```kotlin
object Settings {
    
    fun saySomethingTrue() = print("Han shot first")
    
}

// Calling the function saySomethingTrue from the singleton class Settings
Settings.saySomethingTrue()
```

The code above represents a singleton class called *Settings* that can be created in a *lazy* way. Everything is handled by Kotlin and you do not need to worry about anything else.

#### Pros

- It ensures an instance control
- Great flexibility to create an instanciation process
- Easy to implement

#### Cons

- It can complicate unit testing
- It is quite hard to manage its life-cycle

