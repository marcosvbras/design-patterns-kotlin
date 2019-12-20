# Factory Method

#### When should I use it?
The Factory Method is used when we do not know beforehand how many types or dependencies we are going to deal with. This pattern is all about creating objects that implement a common interface given a certain type passed as parameter. We create objects without exposing the creation logic to the client code.

#### Implementation

First of all, you need to create classes that implement either the same interface or parent class. This interface/class will be the high-level type of object that your factory will create. In the example below, the high-level type is **User** and its subtypes are **Teacher** and **Student**:

```kotlin
interface User {
    val name: String
}

class Teacher : User {
    val name = "Ned Stark"
}

class Student : User {
    val name = "Jon Snow"
}

```

Then, you create a class with a creator method. This one receives an object type and decides what it is going to be creared.

```kotlin
class UserFactory {
    
    fun createUser(userType: UserType): User = when(userType) {
        UserType.STUDENT -> Teacher()
        UserType.TEACHER -> Student()
    }
    
}

val userFactory = UserFactory()
val englishTeacher = userFactory.createUser(UserType.TEACHER)
print(englishTeacher.name)
```

#### Pros

- By moving object creation into one place in the program increases the *Single Responsibility Principle*
 You avoid tight coupling between the creator and the concrete products.
- Reduces coupling between the object creator and the use of the objects
- Use of *Open/Close Principle* since you can insert new types into the Factory without breaking the existing cliend code that uses the Factory

#### Cons

- The code may become more complicated since you need to introduce a lot of new subclasses to implement a factory.

