# Builder

The *Builder* pattern is a useful paradigm in the Java programming language when there are many parameters needed to construct an object. As Effective Java points out, constructors or factory methods with too many parameters become susceptible to bugs when parameters are accidentally swapped in clients. Also, with lots of parameters, you will have to set at least `null` everytime you do not need to that certain parameter. This pattern in Kotlin is kind of an anti-pattern, because there are a lot of language features that make Builders redundant, like named and default parameters.

In the *Builder* pattern you must:
- Set a default value that makes contextual sense for the given problem. If there is no appropriate default value and you want to ensure the caller sets a value, use lateinit, or some other validity measure
- Enforce setting a value on required fields through a constructor to have a safer implementation

#### Implementation

```kotlin
data class Account(
    val email: String,
    val password: String,
    val fullName: String = "",
    val country: String = "",
    var phoneNumber: String = ""
) {

    class Builder(private val email: String, private val password: String) {

        private var _fullName: String = ""
        private var _country: String = ""
        private var _phoneNumber: String = ""

        fun fullName(fullName: String): Builder {
            _fullName = fullName
            return this
        }

        fun phoneNumber(phoneNumber: String): Builder {
            _phoneNumber = phoneNumber
            return this
        }

        fun country(country: String): Builder {
            _country = country
            return this
        }

        fun build(): Account = Account(email, password, _fullName, _country, _phoneNumber)

    }

}

val account = Account.Builder("darthvader@empire.com", "luke")
    .country("Brazil")
    .phoneNumber("(66) 66666-6666")
    .build()

print(account.phoneNumber)
```

#### Pros

- Possibility to construct objects step-by-step, defer construction steps or run steps recursively
- You can isolate complex construction code from the business logic (Single Responsibility Principle)

#### Cons

- You have to remember to update two places when adding a new field since now you have all fields duplicated in the class that is going to be built and the *Builder* class.

