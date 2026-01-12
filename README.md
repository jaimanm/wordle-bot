# Wordle Bot 🎯

An intelligent Wordle solver that uses letter frequency analysis to crack any Wordle puzzle efficiently. This program analyzes a database of all valid Wordle answers and guesses to systematically solve puzzles in an average of ~4.5 attempts.

## How It Works

The bot uses a three-step strategy to find the optimal solution:

1. **Filter** - Narrow down possible guesses using clues from the previous guess
2. **Rank** - Score remaining words using letter frequency analysis 
3. **Guess** - Select the highest-scoring word as the next guess

This process repeats until the correct word is found.

## Strategies

The bot supports two different scoring methods that you can choose from:

### Method 1: Global Letter Frequency
Uses overall letter frequency across all Wordle answers. This method considers how often each letter appears in the entire word list, regardless of position.

### Method 2: Positional Letter Frequency (Default)
Analyzes letter frequency **by position** in the word. For example, 'S' is most common in position 1, while 'E' is most common in position 5. This method provides more accurate predictions by accounting for letter placement patterns.

**Performance**: Method 2 achieves an average of **4.55 tries** across 1000 test games with a maximum of 11 tries.

## Running the Bot

The notebook provides several ways to use the bot:

### Interactive Solver Mode

Help solve a real Wordle puzzle interactively:

```python
solve(method=2)
```

**Usage:**
1. Enter your first guess (or press Enter to use the bot's suggestion)
2. After each guess, enter the clues from Wordle as a 5-digit number:
   - `0` = Grey (letter not in word)
   - `1` = Yellow (letter in word, wrong position)
   - `2` = Green (correct letter, correct position)
3. The bot will suggest the best next guess
4. Type `quit` to exit

**Example:**
```
Enter first guess: slate
Enter clues: 01020
Best Guess: crate
```

### Automated Testing Mode

Test the bot's performance on random Wordle puzzles:

```python
# Single game with display
runWordle(numTimes=1, display=True, method=2)

# Batch testing (1000 games)
triesLog = runWordle(1000, display=False, method=2)
analyze(triesLog)
```

**Parameters:**
- `numTimes`: Number of games to simulate (default: 1)
- `display`: Show step-by-step output (default: True)
- `firstWord`: Specify a custom starting word (default: bot's best guess)
- `method`: Choose scoring strategy - 1 or 2 (default: 2)

### Performance Analysis

After running batch tests, use the `analyze()` function to see statistics:

```python
analyze(triesLog)
```

This displays:
- Mean number of tries
- Standard deviation
- Min/max attempts
- 25th, 50th, and 75th percentiles

## Getting Started

### Prerequisites
- Python 3.x
- NumPy
- Pandas
- Jupyter Notebook (to run the .ipynb file)

### Installation

1. Clone this repository:
```bash
git clone https://github.com/jaimanm/wordle-bot.git
cd wordle-bot
```

2. Install dependencies:
```bash
pip install numpy pandas jupyter
```

3. Launch Jupyter Notebook:
```bash
jupyter notebook wordle.ipynb
```

## Data Files

The bot uses two data files located in `wordle_data/`:
- `wordle-answers-alphabetical.txt` - Complete list of valid Wordle answers
- `wordle-allowed-guesses.txt` - Extended list of acceptable guess words

## Algorithm Details

The bot's intelligence comes from:
- **Frequency Analysis**: Pre-computed letter frequency tables for each position
- **Smart Filtering**: Efficient elimination of impossible words after each clue
- **Duplicate Handling**: Penalty system for words with duplicate letters to maximize information gain

## Performance

Based on 1000 simulated games using Method 2:
- **Average**: 4.55 tries
- **Median**: 4 tries
- **Success Rate**: 100% within 11 tries
- **Within 6 tries**: ~98% (standard Wordle limit)

## License

This project is available for personal and educational use.

## Author

Created by [Jaiman Munshi](https://github.com/jaimanm)

---

*Visit my [personal website](https://jaimanm.github.io) to see more projects!*
