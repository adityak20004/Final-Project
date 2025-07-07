# Final-Project
import random
import csv
from collections import Counter

class Dice:
    def __init__(self, sides=6):
        self.sides = sides
    
    def roll(self):
        return random.randint(1, self.sides)
    
class DiceGame:
    def __init__(self, num_rolls=10):
        self.dice = Dice()
        self.num_rolls = num_rolls
        self.results = []
    
    def play(self):
        self.results = [self.dice.roll() for _ in range(self.num_rolls)]
    
    def analyze(self):
        freq = Counter(self.results)
        for face in sorted(freq):
            print(f"Rolled {face}: {freq[face]} times")
    
    def save(self, filename= 'results.csv'):
        with open(filename, 'w', newline= '') as file:
            writer = csv.writer(file)
            writer.writerow(['Roll#', 'Result'])
            for i, val in enumerate(self.results, start=1):
                writer.writerow([i, val])
            print(f"Saved to {filename}")
def main():
    game = DiceGame(num_rolls = 30)
    game.play()
    game.analyze()
    game.save()
    
if __name__ == "__main__":
    main()
