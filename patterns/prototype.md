# Prototype

There are some cases where it is not possible just to create a new object and copy the property values from another object of the same type, since an object can have private properties. Also on this approach, if a new property is included in the class, it is pretty much easy to forget to include this property in some place that is making a copy.

The **Prototype** pattern is all about creating an exact copy of an object being able to make slight changes. It delegates the cloning process to the actual objects that are being cloned. The pattern declares a common interface for all objects that support cloning. An object that supports cloning is called a *prototype*.

The implementation of the clone method is very similar in all classes. The method creates an object of the current class and carries over all of the field values of the old object into the new one, being possible to copy even the private properties, since these ones are in the same scope as the clone method.

#### Implementation

To implement a Prototype pattern in Kotlin is really simple, since the programming language itself already provides an implementation through the method `copy`. For example, to create a new copy of an instance of *Visitor*, you can just call the method `copy` passing the values you want to change:

```kotlin
data class Visitor(val date: String, val identification: String, val isVip: Boolean)

val ordinaryVisitor = Visitor("12/30/2019", "123456790", false)
val famousVisitor = ordinaryVisitor.copy(isVip = true)
```

#### Pros

- You can get rid of repeated initialization code
- Possibility to recreate complex objects more conveniently

#### Cons

- Cloning complex objects that have circular references might be very tricky

