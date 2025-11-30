# IA3_Proiect
Adversarial Attacks & Defense Mechanisms for Spam Classification

This project explores how a neural spam classifier behaves under adversarial conditions and how different defense strategies improve robustness. The work combines practical attack implementations with defense evaluation on the Enron email dataset.

 Project Summary

We train a lightweight spam classifier using:

-Trainable word embeddings

-GlobalAveragePooling

-Dense classifier

The goal is to measure how this model reacts to adversarial manipulations and how defense mechanisms compensate.

The project includes:

-two attacks: TextFooler (synonym-based) and HotFlip (gradient-driven)

-two defenses: Feature Squeezing and Adversarial Training

-a combined defense evaluation

Baseline Model

The original spam classifier reaches high performance on clean data:

Clean Accuracy ≈ 98%

However, it is vulnerable to small textual perturbations.

TextFooler Attack (Our Implementation)

We implement a synonym-based black-box attack inspired by TextFooler:

-identifies important tokens based on probability drop

-replaces them with WordNet synonyms

-preserves semantic meaning

-repeats until the predicted label flips or limit reached

Baseline results (before defenses):

-Success: 4 flips out of 20 attacked emails

-Strict ASR = 20%

-18/20 samples were modified (flip + near-adversarial)

The model is clearly sensitive to synonym substitutions even in cases where it does not flip its prediction.

 HotFlip Attack (White-Box)

HotFlip is a gradient-based attack that uses directional derivatives to find the most impactful character or word modification.

Baseline resistance:

-HotFlip still manages to cause misclassifications

-ASR noticeably higher than desirable

 Defense 1 — Feature Squeezing

Feature Squeezing reduces variability in the input by collapsing rare or unusual tokens into a single placeholder token.

Implementation:

-Compute token frequencies on the training corpus

-Replace all other tokens with a placeholder

-Wrap this transformation in the prediction pipeline

-ASR decreases significantly compared to baseline

-Feature Squeezing limits the attacker’s ability to exploit semantic-level variations.

 Defense 2 — Adversarial Training (Most Effective)

We generate adversarial and near-adversarial TextFooler examples from the training set and mix them with the original clean data.

A new model is trained from scratch using this augmented dataset.

