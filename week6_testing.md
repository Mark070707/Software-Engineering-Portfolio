# Software Engineering Week6 submission

## The Task

The practical exercise in week 6 involved competitive testing. For your portfolio entry,
select two pieces of test code that you wrote that best illustrate your skills in this
area.

For each example

* Summarise the purpose of the code you were testing
* Include the test code
* Provide a brief explanation of the test(s) that are performed
* Explain why this is an important aspect of the code to test
* Identify any limitations of your tests (this may be something that you realised after
  the evaluation).

Did you manage to write a test which failed during the final evaluation? If so, that would
make an excellent example. You should briefly discuss why the writer of the code might 
have overlooked the particular test case that failed.


## Test Case 1

Testing the CheckLetterInWord Function
Purpose: To ensure that the CheckLetterInWord function correctly identifies whether a guessed letter is in the word.

```
[Fact]
public void TestCheckLetterInWord()
{
    // Arrange
    GamePage game = new GamePage("Easy");
    game.Word = "apple";

    // Act
    bool isCorrect1 = game.CheckLetterInWord("apple", 'a');
    bool isCorrect2 = game.CheckLetterInWord("apple", 'b');

    // Assert
    Assert.True(isCorrect1, "Correct letter 'a' should be identified.");
    Assert.False(isCorrect2, "Incorrect letter 'b' should not be identified.");
}
```
Explanation: This test checks if the CheckLetterInWord function can correctly identify
whether a guessed letter is present in the target word. It tests for both a correct and an incorrect guess.

Importance: This is crucial because the game's core functionality depends on correctly identifying
whether the guessed letter is in the word. If this function fails, it would lead to incorrect game behavior.

Limitations: This test assumes that the CheckLetterInWord function handles correct and incorrect letters properly.
Real-world tests would need to cover more edge cases and validate the function for different word lengths and game types.


## Test Case 2

Testing the GameOver Function
Purpose: To ensure that the GameOver function correctly determines the game outcome.

```
[Fact]
public void TestGameOver()
{
    // Arrange
    GamePage game = new GamePage("Easy");
    game.Word = "apple";

    // Act
    game.CorrectLetters = new List<char> { 'a', 'p', 'l', 'e' };
    game.GameOver(); // Winning scenario

    game.CorrectLetters = new List<char> { 'a', 'p', 'r', 'e' };
    game.GameOver(); // Losing scenario

    // Assert
    Assert.True(game.GameOutcome == GameOutcome.Win, "The player should win if all letters are guessed.");
    Assert.True(game.GameOutcome == GameOutcome.Lose, "The player should lose if not all letters are guessed.");
}
```
Explanation: This test checks if the GameOver function correctly determines the game outcome (win or lose) based
on the correct letters guessed. It tests both winning and losing scenarios.

Importance: It's essential to verify that the GameOver function accurately determines the game outcome,
as this is what informs the player whether they've won or lost. Incorrect game outcomes could lead to a poor user experience.

Limitations: This test is somewhat simplistic and assumes that the GameOver function solely relies on the correct letters guessed.
In a real-world scenario, you may have more complex win/lose conditions, such as the number of attempts or time limits.
The test should be expanded to cover such conditions.