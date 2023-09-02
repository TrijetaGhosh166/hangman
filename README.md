# hangman

 import random

class Hangman:
    def __init__(self, wordlist):
        self.wordlist = wordlist
        self.word = " "
        self.guesses = []
        self.max_attempts =4
        self.attempts = 0
        self.current_guess = '_' * len(self.word)
        self.guessed_letters = set()
        self.status = "INCOMPLETE"
    
    def get_word(self):
        self.word = random.choice(self.wordlist).upper()
    
    def display(self):
        print(f"Current guess: {self.current_guess}")
        print(f"Guessed letters: {' '.join(sorted(self.guessed_letters))}")
        print(f"Wrong guesses: {self.attempts}/{self.max_attempts}")
        
    def guess(self, letter):
        letter = letter.upper()
        if letter in self.guessed_letters:
            return
        self.guessed_letters.add(letter)
        if letter in self.word:
            for i in range(len(self.word)):
                if self.word[i] == letter:
                    self.current_guess = self.current_guess[:i] + letter + self.current_guess[i+1:]
        else:
            self.attempts += 1
        
    def over(self):
        return self.attempts >= self.max_attempts or self.current_guess == self.word
    
    def play(self):
        print(" !!! WELCOME TO HANGMAN GAME !!!\n ")
        print(" YOU HAVE TO ENTER A COLOUR NAME --")
        self.get_word()
        while not self.over():
            self.display()
            guess = input("GUESS A LETTER OF THE COLOUR: ")
            self.guess(guess)
        self.display()
        if self.current_guess == self.word:
            print("CONGRATULATIONS! YOU WON!")
        else:
            print(f"SORRY, YOU LOST THE GAME. THE WORD WAS {self.word}")





wordlist=["yellow","white","black","green","brown","peach"]
game=Hangman(wordlist)
game.play()
