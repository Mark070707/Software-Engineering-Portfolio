# Documentation

## The Task

First, choose six rules of clean code and explain them. For each one,

* Summarise the rule in your own words.
* Provide an example from the code that you wrote in week 2 and then refined in week 4.
* Explain how your code implements the rule. 

Second, copy the doxygen comments from your code into your portfolio and provide some 
descriptive commentary on their purpose and structure. Use screenshots showing the HTML 
content that is generated from your code to illustrate your explanation.

Finally, highlight three examples from your code where you have eliminated the need
for comments by adhering to the principles of clean code.

### Meaningful Names
When you create variables, functions, classes, or modules, give them names that clearly explain their purpose.
Descriptive names make code easy to understand.

### Keep Functions and Methods Small
Make sure that functions and methods have a single task.
They should do one thing which simplifies testing, and upkeep of the code.

### Comments Shouldn't Lie
If you use comments in your code, make sure they reflect what the code does.
Outdated or misleading comments can lead to confusion and errors.

### Single Responsibility Principle (SRP):
Each class or module should serve a single purpose, which enhances maintainability.

### Don't Repeat Yourself (DRY)
Duplication code in multiple places can make maintenance difficult and introduce the risk of errors.
Instead, use functions, classes, or modules to encapsulate and reuse code.

### Test-Driven Development (TDD)
Write tests before you write the actual code. This practice ensures that your code functions correct and helps
catch issues when you make changes later on.

### My Code
```
public void Register(string username, string password)
{
    var salt = CreateSalt();
    var hashedPassword = HashPasswordWithSalt(password, salt);
    SaveToDatabase(username, hashedPassword, salt);
}

public bool Login(string username, string password)
{
    var user = GetUserFromDatabase(username);
    var hashedPassword = HashPasswordWithSalt(password, user.Salt);

    return user.HashedPassword == hashedPassword;
}

private string HashPasswordWithSalt(string password, string salt)
{
    // Combine the password and salt and then hash them
    return HashPassword(password + salt);
}

```


## Implimenting The Rule

## Meaningful Names
I've used clear and descriptive method and variable names like Register, Login, HashPasswordWithSalt,
and hashedPassword. This helps me understand my code better.

## Keep Functions and Methods Small
Both Register and Login methods are short and focused on their respective tasks, making them easy to understand and maintain.

## Single Responsibility Principle (SRP)
Each of my Register and Login methods follows the SRP. They have specific responsibilities - one for user registration and
the other for user login.

## Don't Repeat Yourself (DRY)
I've encapsulated the password hashing logic in the HashPasswordWithSalt method to avoid duplicating the code.
This promotes code reuse.

## Comments Shouldn't Lie
While I haven't included comments in my code, I believe my method and variable names are descriptive enough to
convey their purpose. However, I'll consider adding comments for more complex parts of the code or to explain any
non-obvious decisions.

## Test-Driven Development (TDD)
My code doesn't include explicit tests, but I can test each method separately to ensure they work as intended.
I'll consider adding tests to follow the Test-Driven Development approach, which helps ensure code correctness.