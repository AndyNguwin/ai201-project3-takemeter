# Project Planning: Steam Review Classification
## Community

### What community did you choose and why?

I chose **Steam game reviews for Wuthering Waves** as my online community. Steam is a popular game distribution platform for PC and allows users to submit reviews on the games they played with an associated recommendation label (ex. "Recommended" vs. "Not Recommended"). I specifically chose **Wuthering Waves** because it's a game that I enjoy playing myself.

### Why is this community a good fit for classification?

Steam reviews are a strong fit for classification because reviews varies widely in:

* sentiment (positive vs negative)
* review length
* level of detail
* writing style

Some reviews are highly detailed and analytical, while others are short emotional reactions or jokes. This variety makes the classification task both challenging and meaningful.

---

## Labels

This classifier uses the following labels:

### Label 1: Positive / Recommend

A review is labeled **Positive / Recommend** if its overall message indicates that the reviewer recommends the game to others, typically emphasizing enjoyable gameplay, satisfying features, or a worthwhile experience despite minor flaws.

#### Example Reviews

* Example 1:

  > "what can I say about this game, it's definitely not bad, I downloaded it only because of the collaboration with cyberpunk. So the storyline in the game is cool, the characters are interesting and beautiful, the music is excellent."

* Example 2:

  > "This is my first gacha game and I have to say I'm very impressed. I gave it a try because it was voted players choice GOTY and I can see why. The combat has a very high skill ceiling and is very satisfying overall, especially when you land combos and counters. I will say the new player experience leaves something to be desired, you get bombarded by UI menus and a million popups and notifications you don't understand, but if you can push through that intial overstimulation this game has a ton of depth and a fantastic story with lots of potential for the future."

---

### Label 2: Negative / Not Recommend

A review is labeled **Negative / Not Recommend** if its overall message indicates that the reviewer does not recommend the game to others, typically emphasizing major flaws such as poor gameplay, technical issues, monetization concerns, or an unsatisfying experience.

#### Example Reviews

* Example 1:

  > "Underwhelming. I was told to "push through" until I reach 2.0 but after having played over 30 hours I just can't be bothered anymore. Not worth it."

* Example 2:

  > "Downloaded 100GB. Launched the game. Downloaded another 15GB. Was asked to restart game. OK, Tried to restart. And... Another 35GB update. I JUST WANTED TO RELAX AND PLAY. Unfortunately at that moment my patience was over. Though game looks beautiful."

## Hard Edge Cases

Some reviews are genuinely ambiguous between the two labels because Steam reviews can sometimes contain mixed sentiment. Reviews can talk about both the good and bad of a game or a user can state they love while pointing out a bad issue they faced.

### Example Ambiguous Review

  > "I love this game, but please please fix it so it works on steam deck - I was so excited to finally play via steam"

### Ambiguous Annotation Rule
If the reviewer ultimately appears to recommend the game despite flaws, it will be labeled Positive; otherwise, it will be labeled Negative.

## Data Collection Plan

- I will scrape 200 total reviews of Wuthering Waves on the Steam page. Each review will be English only and cleaned to have no odd, non-ASCII characters and reviews must be text-only. Because reviews are always categorized as "Positive" and "Negative", I can filter the scraping to scrape 100 of each label.

## Evaluation Metrics
For evaluation, it's important to have the overall accuracy but also **precision**, **recall**, and **F1 score**. Extra metrics such as **precision**, **recall**, and **F1 score** provides extra details regarding the accuracy of the model, allowing us to understand what mistakes the model makes when classifying.

- **Accuracy per class**: Overall percentage of correct predictions per class.
- **Precision**: Percentage of predictions for each class being correct. A high precision means that when the model assigns a label, it is usually correct.
- **Recall**: Percentage of actual examples in each class that were identified correctly. A high recall means that the model successfully identified most examples belonging to that class. 
- **F1 Score**: A measure of the balance between the model's precision and recall. High recall and low precision means the model biases a label when classifying. High precision and low recall means the model predicts a label only when it is highly confident.


## Definition of Success

In my opinion, 75% is what I would consider an acceptable threshold, similar to average grades (C range is usually 70-79%).

- MINIMUM:
  - Accuracy >= 75%
  - F1 Score >= 0.75
  - Recall >= 0.75
 
- GOAL:
  - Accuracy >= 85%
  - F1 Score >= 0.85
  - Recall >= 0.85


