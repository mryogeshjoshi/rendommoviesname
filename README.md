import random

def choose_movie():
    # List of Bollywood movie titles
    bollywood_movies = [
        "Sholay",
        "Dilwale Dulhania Le Jayenge",
        "Kabhi Khushi Kabhie Gham",
        "3 Idiots",
        "Lagaan",
        "Zindagi Na Milegi Dobara",
        "Dangal",
        "Bajrangi Bhaijaan",
        "Queen",
        "PK"
    ]
    # Randomly select a movie
    return random.choice(bollywood_movies)

def display_word(movie, guessed_letters):
    # Show the movie title with guessed letters and underscores for unguessed letters
    display = ''.join(letter if letter.lower() in guessed_letters or not letter.isalpha() else '_' for letter in movie)
    return display

def start_game():
    # Choose a random movie
    movie = choose_movie()
    # Initialize guessed letters and incorrect guesses
    guessed_letters = set()
    incorrect_guesses = 0
    max_incorrect_guesses = 6  # Maximum number of incorrect guesses allowed

    print("Welcome to the Bollywood Movie Guessing Game!")
    print("Guess one letter at a time.")
    
    while incorrect_guesses < max_incorrect_guesses:
        # Display the current state of the movie title
        current_display = display_word(movie, guessed_letters)
        print(f"Movie: {current_display}")
        print(f"Incorrect guesses left: {max_incorrect_guesses - incorrect_guesses}")
        
        # Get player's letter guess
        guess = input("Enter a letter: ").strip().lower()
        
        # Check if the input is a single alphabet letter
        if len(guess) != 1 or not guess.isalpha():
            print("Please enter a single letter.")
            continue
        
        # Check if the letter has been guessed before
        if guess in guessed_letters:
            print("You've already guessed that letter.")
            continue
        
        # Update guessed letters
        guessed_letters.add(guess)
        
        # Check if the letter is in the movie title
        if guess in movie.lower():
            print("Good guess!")
        else:
            print("Incorrect guess.")
            incorrect_guesses += 1
        
        # Check if the player has guessed all letters
        if all(letter.lower() in guessed_letters or not letter.isalpha() for letter in movie):
            print(f"Congratulations! You've guessed the movie: '{movie}'")
            break
    else:
        print(f"Sorry, you've run out of attempts. The correct movie was: '{movie}'")

if __name__ == "__main__":
    start_game()
