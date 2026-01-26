# Automated Stimulus Selection for Linguistic & Social Cognition Research

This project provides a Python-based pipeline to automate the selection of balanced linguistic stimuli for my lab's behavioral and neuroscience studies. It solves the complex task of matching word groups across multiple statistical constraints. 

## Project Overview

Previously, the **Language Comprehension Lab at Central European University (CEU)** developed a dataset consisting of 240 verbs, rated across two-dimensions of "sociality" measures: **Mutuality** and **Jointness** (Srdoc, Marx, & Wittenberg, 2025; Srdoc, Marxi, Safrany et al., 2025).

*   **Mutuality**: Evaluates if an action is inherently performed together by multiple participants (e.g., *to talk*).
*   **Jointness**: Evaluates if an action is specifically directed toward another person (e.g., *to hug*).

We are preparing a follow-up study where we need a balanced linguistic prime set. This algorithm builds on those 240 verbs' data to automate the selection of these stimuli, ensuring that the selected groups are statistically identical in terms of confounding variables.

## Target Stimuli Categories

The tool selects 15 items for each of the following categories:

*   **Social Verbs**: Actions involving high social interaction (e.g., *to date, to collaborate, to chat*).
*   **Non-Social Verbs**: Actions typically performed alone (e.g., *to run, to sleep, to swim*).
*   **Inanimate Nouns**: Objects with no biological or social agency (e.g., *table, hammer, book*).

All groups are balanced for **Word Frequency** (Log-transformed) (extracted from SketchEngine: enTenTen21, huTenTen23, deTenTen23 - not the up-to-date version, but the obsolete to match the LISADA database), **Emotional Valence**, and **Arousal** (EnglishLexicon: https://elexicon.wustl.edu/) across three languages: **English, German, and Hungarian**.

## Key Features

1.  **Automated Noun Generation**: Instead of manual collection, the script uses **NLTK and WordNet** to extract a large pool (~300) of inanimate nouns (e.g., filtered by 'artifact.n.01'), significantly increasing the mathematical chance of finding a balanced set.
2.  **Iterative Balancing Algorithm**: A custom solver that uses random sampling and simultaneous **independent t-tests** to validate the stimulus sets.
3.  **Statistical Rigor**: The algorithm only accepts a list if **all p-values are > 0.05** across all control variables and all categories.

## Tech Stack

*   **Python** (Pandas, NumPy) for data manipulation.
*   **NLTK (WordNet)** for automated linguistic pool expansion.
*   **SciPy (stats)** for the t-test-based validation logic.
*   **GoogleTranslator API** for cross-referencing inanimate nouns across languages.

## How the Balancing Works

1.  **Pool Creation**: The script prepares pools for the three categories (Social, Non-Social, Inanimate).
2.  **Random Sampling**: It picks 15-15-15 words at random.
3.  **Validation**: It runs t-tests between all pairs (e.g., Social vs. Inanimate) for every metric (Frequency, Valence, Arousal).
4.  **Iteration**: If any p-value is below 0.05 (meaning a significant difference exists), it discards the set and tries again.
5.  **Output**: Upon success, it exports a `balanced_stimuli_lists.xlsx` file ready for experimental use.

## 📄 References

*   Srdoc, T., Marx, E., & Wittenberg, E. (2025). Event construal through social verbs in English and German: The LISADA corpus. Processings of the Cognitive Science Society Annual Meeting (Vol. 47). 

*   Srdoc, T., Marx, E., Safrany, A. V., Balla, A., & Wittenberg, E. (2025). Linguistic Impact on Social Action Construal Database (LISADA). https://osf.io/xzdqc/

