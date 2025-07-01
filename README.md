# Language Classification using Decision Tree & AdaBoost

## Overview

This project implements a language classifier that distinguishes between English and Dutch text using two machine learning approaches:

- **Decision Tree** (with entropy and information gain for attribute selection)  
- **AdaBoost** (adaptive boosting with decision stumps)

The classifier uses various handcrafted linguistic features extracted from text samples to train and predict language labels.

---

## Features Used

- Average word length in a statement  
- Presence of English articles (`an`, `the`)  
- Presence of Dutch diphthongs (e.g., `ae`, `ei`, `au`, etc.)  
- Presence of common Dutch words  
- Presence of common English words  
- Detection of non-English characters/symbols  

These features form a numeric feature vector for each text input, which the classifiers use to learn and predict.

---

## How It Works

### Decision Tree

- Uses entropy and information gain to select the best attribute for splitting data.
- Builds a tree recursively until max depth or no information gain.
- Predicts language by traversing the tree based on feature values.

### AdaBoost

- Combines multiple weak classifiers (decision stumps).
- Each stump focuses on weighted training examples emphasizing previous errors.
- Final prediction is a weighted vote of stumps.

---

## Usage

The program runs in two modes: **train** and **predict**

# Training
```
python your_script.py train <training_data_file> <hypothesis_output_file> <learning-type>
```

# Predicting
```
python your_script.py predict <hypothesis_file> <test_data_file>
```

- ```<learning-type>```: Either dt for Decision Tree or ada for AdaBoost.
- Training file format: Each line contains a label and statement separated by |, e.g., 
  en|This is an example sentence. 
  nl|Dit is een voorbeeldzin.
- Prediction file format: Each line contains only a statement (no label).

---

## Implementation Details
- Training builds and serializes a hypothesis model to a file using pickle.
- Prediction loads the hypothesis file and classifies input statements.
- Features are extracted via the get_features function from features.py.
- Decision Tree nodes are represented using a Node dataclass.
- AdaBoost iteratively trains decision stumps and adjusts sample weights.
