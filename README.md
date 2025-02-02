import random

def choose_word():
    word_list = ["apple", "banana", "orange", "grape", "kiwi", "mango", "pineapple", "strawberry", "watermelon"]  # Expand this list!
    return random.choice(word_list).lower()

def display_word(word, guessed_letters):
    displayed_word = ""
    for letter in word:
        if letter in guessed_letters:
            displayed_word += letter + " "  
        else:
            displayed_word += "_ "
    return displayed_word

def hangman():
    
    word_to_guess = choose_word()
    guessed_letters = set()  # Use a set for efficient checking
    incorrect_guesses_left = 6  # Set the number of allowed incorrect guesses

    print("Welcome to Hangman!")
    print("Try to guess the word")
    while True:
        print("\n" + display_word(word_to_guess, guessed_letters))
        print(f"Incorrect guesses left: {incorrect_guesses_left}")

        guess = input("Guess a letter: ").lower()

        if len(guess) != 1 or not guess.isalpha():
            print("Invalid input. Please enter a single letter.")
            continue

        if guess in guessed_letters:
            print("You've already guessed that letter.")
            continue

        guessed_letters.add(guess)

        if guess not in word_to_guess:
            incorrect_guesses_left -= 1
            print("Incorrect guess.")

        if "_" not in display_word(word_to_guess, guessed_letters):
            print(f"\nCongratulations! You guessed the word: {word_to_guess}")
            print("You Won the game")
            break

        if incorrect_guesses_left == 0:
            print(f"\nYou ran out of guesses. The word was: {word_to_guess}")
            break

if __name__ == "__main__":
    hangman()
