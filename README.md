Strategy Overview
The strategy leverages statistical language modeling, specifically n-gram models, to predict the next letter in a word. N-gram models capture the probabilities of letter sequences in words. The approach progressively considers unigram (single letter), bigram (two letters), trigram (three letters), fourgram (four letters), and fivegram (five letters) probabilities to make an educated guess about the next letter.

Steps in the Strategy
Cleaning the Input Word:

The input word is provided in a format like "_ p p _ e ". Spaces are removed to get a clean word format like "_pp_e".
Tracking Incorrect Guesses:

Incorrect guesses are tracked to update the n-gram models accordingly, ensuring that words containing incorrectly guessed letters are eliminated from consideration.
Building N-gram Models:

Unigram: Counts the occurrences of individual letters in the dictionary.
Bigram: Counts the occurrences of every pair of consecutive letters.
Trigram: Counts the occurrences of every sequence of three consecutive letters.
Fourgram: Counts the occurrences of every sequence of four consecutive letters.
Fivegram: Counts the occurrences of every sequence of five consecutive letters.
Reoptimizing N-grams:

When an incorrect guess is made, the n-gram models are reoptimized by excluding words containing the incorrectly guessed letters from the dictionary and rebuilding the n-gram models.
Calculating Probabilities:

Fivegram Probability:

The model first attempts to match sequences of four known letters and one unknown letter, considering different positions of the unknown letter within the sequence.
Probabilities for each letter are updated based on the occurrences of matching five-letter sequences.
The fivegram probabilities are interpolated with lower-level n-gram probabilities to balance the influence of different n-gram levels.
Fourgram Probability:

Similar to the fivegram probability but considers sequences of three known letters and one unknown letter.
Probabilities are updated based on the occurrences of matching four-letter sequences.
These probabilities are interpolated with the existing probabilities.
Trigram Probability:

Focuses on sequences of two known letters and one unknown letter.
Probabilities are updated based on the occurrences of matching three-letter sequences.
Interpolates these probabilities with the existing probabilities.
Bigram Probability:

Focuses on sequences of one known letter and one unknown letter.
Probabilities are updated based on the occurrences of matching two-letter sequences.
Interpolates these probabilities with the existing probabilities.
Unigram Probability:

Considers the frequency of each letter appearing in the dictionary.
Probabilities are updated based on the occurrences of individual letters.
Interpolates these probabilities with the existing probabilities.
Interpolating Probabilities:

The probabilities obtained from higher-level n-grams are combined (interpolated) with those from lower-level n-grams using predefined weights:
Fivegram: 40%
Fourgram: 25%
Trigram: 20%
Bigram: 10%
Unigram: 5%
This step balances the influence of different n-gram models to make a more accurate prediction.
Guessing the Next Letter:

After calculating and interpolating the probabilities, the letter with the highest probability is selected as the next guess.
Example Flow
The input word "_pp_e" is cleaned to "_pp_e".
The model updates the list of incorrect guesses if the last guessed letter was wrong.
N-gram models are built or reoptimized based on the current dictionary.
Probabilities for each letter are calculated using the fivegram model and interpolated with lower-level n-gram probabilities.
The process continues down to unigram probabilities.
The final probabilities are normalized.
The letter with the highest probability is guessed.
Summary
The strategy combines n-gram models of varying lengths to capture both local and global patterns in the word. By iteratively refining the probabilities and balancing the influence of different n-gram levels, the model can make informed guesses about the next letter, improving its accuracy over time.
