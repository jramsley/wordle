# Wordle
## Introduction
Wordle is a game that is hosted by the New York Times located at https://www.nytimes.com/games/wordle/index.html.  The object of the game is to guess the mystery 5 letter word in as few guesses as possible.  A player will have 6 guesses to guess the word and if they are not able to they fail to win the game.

When a user guesses a word, a couple of clues are used to help facilitate the next possible guesses:
* If a letter guessed is not in the mystery word it will be listed as grey.  This indicates next guesses should omit these letters if they are going to correctly guess the word
* If a letter guessed is in the word, but not in the right position, it is listed as yellow.
* If a letter guessed is in the word and in the right position, it is listed as green
* Each guess will stay shown and allow the user to reference it to help facilitate their next guess.

 A user will guess by entering a 5 letter word and pressing **enter**.  This will submit the word and the game will determine which letters are correct, which letters exist but are in the wrong position, and which letters exist and are in the right position.  The game ends when the user either gets all of the letters right in the right position or they run out of their 6 guesses.

A caveat to the guesses is that a letter can show up multiple times.  For example, the word **seven**, the letter **e** is shown up multiple times.  If the user enters **bikes** as the guess, the **e** will be green because it is in the right location there, but that doesn't indicate it isn't also elsewhere in the word.

## Phase 1 - Initial game
The first phase of this project is to build a command line game for Wordle.  What should be submitted is:
* A python program that a user can execute to start the game
* A hardcoded 5 letter word will be used (you decide)
* A prompt will tell a user to enter a 5 letter word; the prompt will also tell them the guesses remaining
ex.
```
guesses remaining: 6
guess: 
```
* After a user submits a guess, it will indicate which letters are correct but in the wrong location with a **\?** and which letters are correct and in the right location with a **\***
ex. (for the word **beets**
```
guesses remaining: 6
guess: bikes

b* i  k  e? s

guesses remaining: 5
guess: breed

b* i  k  e? s
b* r  e* e? d
```
* If the user guesses the word correctly, a prompt returns telling them they correctly guessed the word
ex. (for the word **beets**
```
guesses remaining: 6
guess: beets

You correctly guessed the word: beets
You took number of guesses: 1
```

## Phase 2 - Error handling
Phase 2 we will update our program from step 1 to do error handling of the user input

1. If a user enters a word that is shorter than 5 letters long, it will be rejected and not count as a guess
ex.
```
guesses remaining: 6
guess: cat

"cat" is less than 5 letters long, try again

guesses remaining: 6
guess:
```
2. If a user enters a word that is longer than 5 letters long, it will be rejected and not count as a guess
```
guesses remaining: 6
guess: icecream

"icecream" is more than 5 letters long, try again

guesses remaining: 6
guess:
```
3. If a user enters input that isn't just letters, it will be rejected and not count as a guess
```
guesses remaining: 6
guess: a dog

"a dog" includes the character(s) " " which is not a letter, try again

guesses remaining: 6
guess:
```

## Phase 3 - Generated word
Wordle is more interesting if a user can run it multiple times and not use the same word every time.  In phase 3, the goal is to use a generated 5 letter word instead of a hardcoded word to guess

OSX/Mac come with a dictionary file located at `/usr/share/dict/words`.  At the start of the game we should:
1. Read in all of the words at `/usr/share/dict/words` and split into individual strings to give us an array of words
2. Remove all words that are not 5-letters long
3. Generate a random number that gives us an index and gets a random 5-letter word
4. Uses this word for the game

## Phase 4 - Documentation/Help
If a user is new to Wordle, we should give instructions on how to play.  If a user enters **help** as an input, we should print out the instructions on how to play.  We should also include documentation with our program to explain how to run the game and how the files are structured

1. Create a file called `README.md` that uses markdown (https://www.markdownguide.org/) for how to start the game and how the files are structured
2. Create a function called `help` that will print out how to play the game is a user enters **help** as the input

## Phase 5 - Tests
python includes a unit test framework called **unittest** (https://docs.python.org/3/library/unittest.html).  We should develop tests for individual functions that are written to validate they won't break as we make changes.

1. Write test steps in plain English
ex.
```
1. Try to call `input_checker` with a word less than 5 letters (like "cat") and validate the number of guesses doesn't increase
2. Try to call `input_checker` with a word larger than 5 letters (like "eleven") and validate the number of guesses doesn't increase
3. Try to call `input_checker` with a word exactly 5 letters long (like "bikes") and validate the number of guesses doesn't increase
```
2. Run through tests manually and save results as pass/fail in a file called `tests.txt`
3. Convert our tests to use **unittest** framework

## Bonus - Colors
When we are indicating wrong/wrong position/correct aspects of letters, we are currently using **\*** and **\?**.  This makes it less readable than just the word entered and difficult to parse compared to the colors used in https://www.nytimes.com/games/wordle/index.html.  As a bonus, we should create a `colorize` function that will use ANSI escape codes to colorize each letter (https://en.wikipedia.org/wiki/ANSI_escape_code).  We should:
1. Color the background of letters that aren't in the word with grey and make the text white
2. Color the background of letters that are in the word but in the wrong position with dark yellow and make the text white
3. Color the background of letters that are in the word and in the right position with dark green and make the text white
