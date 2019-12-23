# Static Factory Method

The Static Factory Method pattern is an variation of [Factory Method](factory.md). Their differences are in the way each one create instances. While in the Factory Method you create an instance of the *factory class* first, the Static Factory Method creates what you expect through a static function to do everything. The main problem with a constructor is that by definition they do not have names, turning into a difficult approach in terms of legibility.

#### Implementation

Kotlin does not use the keyword `static` to declare static functions, another pair of keywords named `companion object` are used instead. The example below is based on the [Factory Method](factory.md) markdown, but adapted with the static behavior:

```kotlin
class User {

    companion object {
        
        fun ofType(userType: UserType): User = when(userType) {
            UserType.STUDENT -> Teacher()
            UserType.TEACHER -> Student()
        }
        
    }
    
}

class Teacher : User {
    override val name = "Ned Stark"
}

class Student : User {
    override val name = "Jon Snow"
}

val englishTeacher = User.ofType(UserType.TEACHER)
print(englishTeacher.name)
```

#### Pros

- The pattern provides better names for the constructor, since it tells exactly what it is expected
- It may provide creation cache
- When calling a Static Factory Method, it may produce either instance of the class or one of its subclasses

#### Cons

- If the class has a private constructor, it can harm inheritance 

