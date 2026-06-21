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

### Annotation Rule
