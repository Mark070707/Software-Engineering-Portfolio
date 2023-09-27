# Software Engineering Week4 submission

## The task

1. Choose the code review challenge which best demonstrates your skills.
2. Copy the code into your portfolio using a Markdown
   [fenced code block](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-and-highlighting-code-blocks).
3. Provide some descriptive commentary that identifies the problems.
4. Show your improved version of the code in a second code block.
5. Explain in one or more paragraphs why your solution is a good one.

## Code review

Code Duplication: Hashing the password with a salt is duplicated in both the Register and
Login methods. This can lead to maintenance issues if changes are needed in the hashing process.

```
public void Register(string username, string password){ 
  var salt = CreateSalt(); 
  var hashedPassword = HashPassword(password, salt); 
  SaveToDatabase(username, hashedPassword, salt); 
} 

public bool Login(string username, string password){ 
  var user = GetUserFromDatabase(username); 
  var hashedPassword = HashPassword(password, user.Salt); 

  if(user.HashedPassword == hashedPassword){ 
    return true; 
  } 
  return false; 
}
```
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

The code duplication has been eliminated by calling the HashPassword method in both the Register
and Login methods.This improved code follows best practices for security and code organization,
making it a easier to maintain.