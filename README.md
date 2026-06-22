# Steam Review Classification
## DEMO VIDEO
- https://www.loom.com/share/d710275650ac40e7b52a2065234cb912
## Community

### What community did you choose?

I chose **Steam game reviews for Wuthering Waves** as my online community. Steam is a popular game distribution platform for PC and allows users to submit reviews on the games they played with an associated sentiment label (ex. "Positive" vs. "Negative"). I specifically chose **Wuthering Waves** because it's a game that I enjoy playing myself.

### Why is this community a good fit for classification?

Steam reviews are a strong fit for classification because reviews varies widely in:

* sentiment (positive vs negative)
* review length
* level of detail
* writing style

Some reviews are highly detailed and analytical, while others are short emotional reactions or jokes. This variety makes the classification task both challenging and meaningful.

---

## Label Taxonomy

This classifier uses the following labels:

### Label 1: Positive

**Definition:**  
A review is labeled **positive** if the overall review expresses satisfaction, enjoyment, or favorable opinions toward the game, even if minor criticisms are present.

#### Examples

| Example | Text | Why this label applies |
| --- | --- | --- |
| 1 | "what can I say about this game, it's definitely not bad, I downloaded it only because of the collaboration with cyberpunk. So the storyline in the game is cool, the characters are interesting and beautiful, the music is excellent." | Highlights the storyline, characters, and music as part of their enjoyment. |
| 2 | "This is my first gacha game and I have to say I'm very impressed. I gave it a try because it was voted players choice GOTY and I can see why. The combat has a very high skill ceiling and is very satisfying overall, especially when you land combos and counters. I will say the new player experience leaves something to be desired, you get bombarded by UI menus and a million popups and notifications you don't understand, but if you can push through that intial overstimulation this game has a ton of depth and a fantastic story with lots of potential for the future." | Speaks deeply in the game mechanics, showing a positive excitement and interest in the game. |

### Label 2: Negative

**Definition:**  
A review is labeled **negative** if the overall review expresses dissatisfaction, frustration, or unfavorable opinions toward the game, even if some positive aspects are acknowledged.

#### Examples

| Example | Text | Why this label applies |
| --- | --- | --- |
| 1 | "Underwhelming. I was told to 'push through' until I reach 2.0 but after having played over 30 hours I just can't be bothered anymore. Not worth it." | Uses the words "underwhelming" and "not worth it", showing disappointment with their experience. |
| 2 | "Downloaded 100GB. Launched the game. Downloaded another 15GB. Was asked to restart game. OK, Tried to restart. And... Another 35GB update. I JUST WANTED TO RELAX AND PLAY. Unfortunately at that moment my patience was over. Though game looks beautiful." | Expresses frustrations with the game's storage size, despite ending off on a highlight. |

---

## Data Collection and Labeling

### Data Collection Source

- **Source:** Steam Store Page (Wuthering Waves)
- **Collection method:** Scraper
- **Total examples collected:** 200 (100 positive, 100 negative)
- **Fields collected:** Text (review itself), label (user sentiment)
- **Filtering/cleaning rules:** English-only, removed empty posts, removed non-ASCII artifacts, text-only

### Labeling Process

- Labels were already assigned by the users themselves when writing the reviews, they were scraped from the store page reviews.
- Because the reviews already come with labels provided by the users when writing the reviews, I won't be manually labelling the reviews myself. However, I will still manually read through each review to note done which reviews may be an ambiguous case that I think the classifier could struggle on, such as reviews that mentions both positive and negative talking points.

### Label Distribution

| Label | Count | Percent |
| --- | ---: | ---: |
| positive | 100 | 50% |
| negative | 100 | 50% |
| **Total** | **200** | **100%** |

### Difficult-to-Label Examples

| Example | Text | True Label | Decision Reasoning |
| --- | --- | --- | --- |
| 1 | "This is definitely one of the better gacha games out currently. I used to be an active Genshin Impact player, but this game caught my eye and I never looked back. The only MAJOR issue I have with this game is the god-awful optimization. For the love of god KURO, PLEASE OPTIMIZE THIS GAME. There is no reason I should be stuttering and having as much frame dropping as I am with my system." | Positive | They say the game is a good game, but they are very focused on a major issue that caused them a lot of trouble, emphasizing "MAJOR" and using the adjective "god-awful" and "no reason to...". The emphasis on the negative pushed me to think it was a negative review. |
| 2 | "Zelda like games burnout is real I am only recommending it because it is a great game with top quality visuals and the combat is actually fun. I am already bored of this game because Genshin made sure that i don't invest my time in useless puzzles, useless dailouge options which never have an impact, bland character personalities. If this is your first gacha game you are lucky, as you will love this game until you reach your burnout point" | Positive | This seems like an odd review to mark as positive since the user points out they are bored and burnt out from this game because of "useless dialogue". It seems like they do think the game is good, but more of a recommendation for others instead of reviewing for their own experience now. |
| 3 | "Wuthering Waves is a great game, especially for a F2P gacha title. It comes close to Expedition 33 in aesthetic and music, or even other AAA games. However, it has three major weaknesses: the 1.x stories havent been polished for a while, theres a lack of end-game content, and the UIs are poor made (turn off the UIs in Septimont and Ragunna to see how good this game could be without those UIs). Even so, with its current foundation, it deserves better. Leaving a negative review after paying and playing and for a long time feels contradictory, but I hope the developers notice that most new players struggle to make it through the 1.x stories because how boring it is. Updated, Spoiler Alert, only read if you've complete the stories and do 100% exploration: + 3.0 (and possibly next versions) is a solid 7.5/10. The main downside is that the story is very predictable and feels mid, not as unique or memorable as Cartethyia, Lupa, Canterella, Phrolova, Iuno, Augusta, Galbrena in 2.x and you know who used to be our Wayfinder and who has been keeping our Shores?. It's not even as good as Encore, they really nailed the 2.x stories and map designs (remember Journeying Paradise?), which fit the characters so well that I doubt they could have done it better. However, 3.0s map design is also outstanding in its own good way, but the school design isn't appeal to me, everything outside the school is gorgeous. Riding a motorbike around the map for exploration feels INSANELY good, the motorbike isn't as clunky as i thought, it literally could fly in the map, and the NPC designs are much better than in 2.x." | Negative | The review keeps swapping between positive and negative. Although the main focus is on the "weaknesses" in the user's experience with the game, I predict it might be difficult for the model to choose because of this mix of highlights and lowlights. |

---

## Fine-Tuning Approach

### Base Model

- **Base model:** distilbert-base-uncased
- **Classification task:** Binary classification

### Training Setup

- **Train/validation/test split:** 70/15/15
- **Number of training examples:** 140
- **Number of validation examples:** 30
- **Number of test examples:** 30
- **Platform**: Google Colab

### Hyperparameter Decision

Describe at least one important hyperparameter decision:

| Hyperparameter | Value | Reasoning |
| --- | ---: | --- |
| Epoch | 15 | With the default of 3, the model wasn't able to train and learn anything substantial yet. I gradually increased it to 5, and eventually to 15 where it seems like the model was no longer making improvements after training. |

---

## Baseline Model
- Groq's llama-3.3-70b-versatile

### Prompt Used

```text
"""
You are classifying Steam game reviews for Wuthering Waves.
Assign each post to exactly one of the following categories.

"Positive": review expresses satisfaction, enjoyment, or favorable opinions toward the game, even if minor criticisms are present.
Example: "what can I say about this game, it's definitely not bad, I downloaded it only because of the collaboration with cyberpunk. So the storyline in the game is cool, the characters are interesting and beautiful, the music is excellent."

"Negative": review expresses dissatisfaction, frustration, or unfavorable opinions toward the game, even if some positive aspects are acknowledged.
Example: "Underwhelming. I was told to "push through" until I reach 2.0 but after having played over 30 hours I just can't be bothered anymore. Not worth it."

Respond with ONLY the label name.
Do not explain your reasoning.

Valid labels:
"Positive"
"Negative"
"""
```

### How Baseline Results Were Collected

- For each review in the test set, the model was given the system prompt and then the text of the review, with the expectation of a single label without any extra commentary.
- **IMPORTANT NOTE**: When gathering the baseline metrics with this model, it got 100% accuracy on all of the test reviews. I wanted to note this down because there's no room for improvement (at least on the accuracy metrics). The reason I suspect it was able to get a perfect test score is because:
  - llama-3.3-70b-versatile is a **powerful** and **pre-trained** model that has strong semantic understand and sentiment association.
  - The problem context might be too simple given that it's a binary classification.
  - Test set size is too small (200) and needs a larger size to see variance. 
---

## Evaluation Report

### Evaluation Setup

- **Test set size:** 30
- **Labels evaluated:** "positive" and "negative"
- **Metrics used:** Accuracy, precision, recall, F1 score, and confusion matrix

Please read the **IMPORTANT NOTE** mentioned in [How Baseline Results Were Collected](#how-baseline-results-were-collected), which discusses the metrics of the baseline test.

### Overall Metrics

| Model | Accuracy | Macro Precision | Macro Recall | Macro F1 |
| --- | ---: | ---: | ---: | ---: |
| Baseline | 1.00 | 1.00 | 1.00 | 1.00 |
| Fine-tuned model | 0.80 | 0.86 | 0.80 | 0.79 |

### Per-Class Metrics: Baseline

| Label | Precision | Recall | F1 Score | Support |
| --- | ---: | ---: | ---: | ---: |
| positive | 1.00 | 1.00 | 1.00 | 15 |
| negative | 1.00 | 1.00 | 1.00 | 15 |

### Per-Class Metrics: Fine-Tuned Model

| Label | Precision | Recall | F1 Score | Support |
| --- | ---: | ---: | ---: | ---: |
| positive | 0.71 | 1.00 | 0.83 | 15 |
| negative | 1.00 | 0.60 | 0.75 | 15 |

### Confusion Matrix: Baseline

Rows are the true labels. Columns are the predicted labels.

| True \ Predicted | positive | negative |
| --- | ---: | ---: |
| positive | 15 | 0 |
| negative | 0 | 15 |

### Confusion Matrix: Fine-Tuned Model

Rows are the true labels. Columns are the predicted labels.

| True \ Predicted | positive | negative |
| --- | ---: | ---: |
| positive | 15 | 0 |
| negative | 6 | 9 |

### Wrong Predictions Analysis

| Example | Text | True Label | Predicted Label | Confidence | Analysis |
| --- | --- | --- | --- | ---: | --- |
| 1 | "Good gameplay, good combat, good visuals, good gacha system. That's it. The story peaked from the start of Rinascita to the end of Cartethyia's story segment (2.0 -> 2.3) and maybe during Phrolova's patch (2.5), but it hit rock bottom after that. Stopping with the companion stories was by far the worst move ever. The main quest just became a "this entire patch's story is all about the new character" simulator. No plot development, lots of yapping, and the story doesn't move forward. It genuinely just feels like a companion quest with some actually important stuff sprinkled here and there (Spoiler alert: It's always Fractsidus). Characters always follow the same pattern: You meet them -> They fully trust you from the first second -> They share their entire life story and trauma dump their generic "muh sad backstory" -> You solve the problems -> "OMG Rover, you're so cool!" -> You find out that you've been in this new region before and were an important figure there, but don't recall it [Generic amnesiac MC#4123] -> Rinse and repeat until another patch comes out, introduces a new character, focuses entirely on them, and completely sidelines the previous one (Certified Chisa moment). It's such a weird state for a game to be in. Quality increases drastically with every patch, but the story only gets worse and worse." | negative | positive | 0.91 | Starts off with stating good features of the game. The review also says quality increases drastically every patch, but only points out problems with the story. |
| 2 | "The game, when you're allowed to play, is pretty damn good. The story, side quests, characters, sounds design, world design, combat... all of it is fantastic. There are two major flaws this game has that stops it from being a 10/10 and drags it down to a solid 5/10.... Gatcha and stamina mechanics. You can have a decent gatcha monetization model that isn't fomo based and incredibly predatory but I have yet to see one and this game is no exception. It's bad and it should feel bad. Stamina is another tactic used by devs to get you to log in regularly and force you to form habits so you're more likely to engage with their monetization model: Gatcha. The main problem is that because these systems exist it strangles it from doing anything else. If it had the freedom to have an actual end game content loop that you WANT to engage with instead of just logging in to put a nickle into your gatcha fund then it would be insanely better. In the end the game is free and it's worth picking up just to enjoy the main story, side stories and to fly around to enjoy the world and music. Just keep in mind what I said above and curve your expectations. "If you're saying it's worth picking up why don't you recommend it then?" Because I f*cking hate stamina systems. It really is such a dumb thing to put in a game." | negative | positive | 0.87 | Review starts off with good highlights and strong positive sentiment (ex. "pretty damn good", "all of it is fantastic"). They even say "it's worth picking p just to enjoy". However, they mark it as a negative review because of two major flaws they wanted to focus on. |
| 3 | "Game started promising, with nice combat and best climbing mechanic I experienced in a while. But with every new major update it became more and more resembling of the typical gachas. Boring exploration because you are given check list and all you have to do is just go to pointed place. Locked features: flying was great, but locked to Rinascita. Than developer added it to the starter territory, but again locked it for a new one. Same with characters. Basically, once next major update is out - you can forget about old characters. There are now new Echo set for each new character. Game currently require no creativity and no thinking, just get latest character, get new echoes and forget about old ones. Really sad to watch such promising game became yet another boring gacha." | negative | positive | 0.51 | Review starts off complimenting the game's features. These words that relate to positive sentiment may have pushed the model to think it might be a positive review, hence the 0.51 confidence despite it focusing on negatives. |

### Sample Classifications

| Example | Text | True Label | Predicted Label | Confidence | Correct? |
| --- | --- | --- | --- | ---: | --- |
| 1 | "Good gameplay, good combat, good visuals, good gacha system. That's it. The story peaked from the start of Rinascita to the end of Cartethyia's story segment (2.0 -> 2.3) and maybe during Phrolova's patch (2.5), but it hit rock bottom after that. Stopping with the companion stories was by far the worst move ever. The main quest just became a "this entire patch's story is all about the new character" simulator. No plot development, lots of yapping, and the story doesn't move forward. It genuinely just feels like a companion quest with some actually important stuff sprinkled here and there (Spoiler alert: It's always Fractsidus). Characters always follow the same pattern: You meet them -> They fully trust you from the first second -> They share their entire life story and trauma dump their generic "muh sad backstory" -> You solve the problems -> "OMG Rover, you're so cool!" -> You find out that you've been in this new region before and were an important figure there, but don't recall it [Generic amnesiac MC#4123] -> Rinse and repeat until another patch comes out, introduces a new character, focuses entirely on them, and completely sidelines the previous one (Certified Chisa moment). It's such a weird state for a game to be in. Quality increases drastically with every patch, but the story only gets worse and worse." | negative | positive | 0.91 | No |
| 2 | "The game, when you're allowed to play, is pretty damn good. The story, side quests, characters, sounds design, world design, combat... all of it is fantastic. There are two major flaws this game has that stops it from being a 10/10 and drags it down to a solid 5/10.... Gatcha and stamina mechanics. You can have a decent gatcha monetization model that isn't fomo based and incredibly predatory but I have yet to see one and this game is no exception. It's bad and it should feel bad. Stamina is another tactic used by devs to get you to log in regularly and force you to form habits so you're more likely to engage with their monetization model: Gatcha. The main problem is that because these systems exist it strangles it from doing anything else. If it had the freedom to have an actual end game content loop that you WANT to engage with instead of just logging in to put a nickle into your gatcha fund then it would be insanely better. In the end the game is free and it's worth picking up just to enjoy the main story, side stories and to fly around to enjoy the world and music. Just keep in mind what I said above and curve your expectations. "If you're saying it's worth picking up why don't you recommend it then?" Because I f*cking hate stamina systems. It really is such a dumb thing to put in a game." | negative | positive | 0.87 | No |
| 3 | "Game started promising, with nice combat and best climbing mechanic I experienced in a while. But with every new major update it became more and more resembling of the typical gachas. Boring exploration because you are given check list and all you have to do is just go to pointed place. Locked features: flying was great, but locked to Rinascita. Than developer added it to the starter territory, but again locked it for a new one. Same with characters. Basically, once next major update is out - you can forget about old characters. There are now new Echo set for each new character. Game currently require no creativity and no thinking, just get latest character, get new echoes and forget about old ones. Really sad to watch such promising game became yet another boring gacha." | negative | positive | 0.51 | No |
| 4 | "I Love this Game! Wuthering Waves grabbed me from the first moment. The attention to detail can be seen in the first few minutes. the mood. the atmosphere, the world and the chracters are created with so much love. the game creates an impressive overall picture of: Story, Graphics, Gameplay and Open World. Story: For me the story has to be exciting and well written so that I can continue playing the game and that is exactly what Wuthering Waves gives me. The more you play the story and discover little clues of the world, you realize how much more deeper Wuthering Waves world and especially story, goes. The Story is gripping, exciting and emotionally. Gameplay: The Gameplay in Wuthering Waves is incredibly fun! The battles fill up powerfully and fluidly, a dynamic of perfect movement and evasion. At the same time it makes exploring the world much more fun. The variety of action and discovery of the world maked the game varied. The World of Wuthering Waves: The world of Wuthering Waves is impressively vibrant and, above all, beautiful! Exploring the Open World is varied and motivating. Wuthering Waves world is a postapocalyptic, yet beautifully reborn landscape shaped by nature. A place where the future and the past meet. Graphics: Wuthering Waves graphic are incredible and the animation are fluid. Wuthering Waves will not disapoint Anime Fans as their style is similar to high-quality Anime. The charactersmodels are finely crafted, with dynamic movements that are particulary evident in combat. The effects of the abilites are clean and color-intensive without cluttering the image. Conclusion: Wuthering Waves is definitely one of my favorite games! The game has grown so much in this one year! Sure, it still has its edges here and there, but you can see how they improve their game each patch. And I hope everyone also sees that Wuthering Waves is created with much love and care in detail, storytelling, gameplay, character design, and open world. And also, that its first and foremost, a incredible good GAME and not just gacha." | positive | positive | 0.96 | Yes |
| 5 | "Worst Optimization in gacha. Have had problems playing this game since release on mobile and desktop. The Game size is GIGANTIC. It is such a large game BOTH on mobile and PC! Over 100BG for a mobile game??? I have to delete other games on my phone just to play it. When I start the game there is always something new to download. It just gets bigger and bigger. Its not worth the effort i spend trying to play this game! Install after install, update after update SOMETHING ALWAYS GOES WRONG. Why is this the only game i play that gives me such difficulty just trying to load it up??? The Devs have no idea what they are doing and still have not fixed the issues present in the game since day 1. I used to think they were better then Genshin devs, but Genshin always runs when i try to play it. This game is LARGER in size than GENSHIN IMPACT. Back to Back banners of BIS units forces you to pull every banner just to have a functional team. Characters are made to work with only certain other characters and if you do not own them, you cannot play certain units to any decent degree of effectiveness. The rewards they gave at the start were great, but not they lock the tiniest rewards behind the most agregious and annoying mini games. I thought genshin was stingy, but WUWA has become just as stingy. Save yourself the headache and play a different gacha game. You'll be able to play 3-4 different gacha games with the space saved from not installing Wuwa. I have played this game since launch and only recently installed the steam version in an attempt to get the game to properly patch and load. IT STILL WONT LOAD OR UPDATE. I have never had an issue install a game via steam.....until i tried to install Wuwa on steam. I though it might've been the Epic launcher at fault...It was not. Its the games fault." | negative | negative | 0.64 | Yes |


### Correct Example Explanation

- From the table above, I will analyze sample classification #4, a positive review that was correctly classified by the model.
- Throughout the whole review, the user describes features of the games very positively and highly, complimenting on things like beautiful graphics and amazing storytelling. The model was highly confident in this (0.96 confidence) because of all of the positive adjectives that the user included in their review.

---

## Reflection

### What did the model learn?

- The model seems to have associated words to the sentiments. Positive words like "good", "amazing", and "fantastic" may sway the model towards positive while words like "boring" and "bad" contribute to negative predictions. It doesn't seem like there's deeper contextual meaning from the combination of words.
- Something that I noticed in the wrong predictions is that it's only the negative reviews that were misclassified as positive. It seems like the model has a bias towards classifying reviews as positive. After investigating the reviews myself, these negative reviews usually followed the pattern of a positive opening before talking about negative experiences that they wanted to focus on. Mixing these two together can make it hard to classify, as I've predicted in my planning doc.

### What did you intend for the model to learn?

- I wanted the model to determine the majority/overall sentiment AND what the focus of the review is. For a human, when reading a review that includes both positive and negative talking points, we can figure out if the sentiment of a review by figuring out what the user wanted to focus on the most. In the pattern of positive start into talking about negative experiences, humans can see that the reviewer wanted to emphasize the negative points in their review.

---

## Spec Reflection

### One way the spec helped

- The specs helped me organize the ideas together from choosing an online community to gather data from, what labels to classify with, the taxonomy definitions, how to evaluate using metrics. Being able to write down my thoughts and ideas while working helped me in my workflow.

### One way implementation diverged from the spec

The original labels I wanted to use were "Positive/Recommended" and "Negative/Not Recommended". However, I eventually decided to just focus on "positive" and "negative" sentiments to clearly dinstinguish between two labels. and their boundaries.

### Why it diverged

I felt like adding the extra nuance of "recommended" and "not recommended" made the label not as clear. It's possible for someone to give a negative review, yet still want to recommend to another user, and vice versa. So, I wanted to simplify the defined boundaries by simplifying the labels as well.

---

## AI Usage

### Instance 1: Data Collection/Scraping

- **What I directed the AI to do:** I asked AI to produce a scraper that scrapes 100 positive and 100 negative Steam reviews for Wuthering Waves, saving the text and label.
- **What the AI produced:** It produced a scraper that scraped any recent reviews for Wuthering Waves, which included non-English reviews and reviews that had non-ASCII characters too.
- **What I revised or overrode:** I revised by stating that the reviews do not have to be recent as there was a new update so new reviews will most likely be of the same topics. I also revised to scrape for English only reviews and reviews to be cleaned.

### Instance 2: Stress Testing Labels

- **What I directed the AI to do:** I provided AI my planning document with my labels to help me test if my labels are easy to distinguish and have clear boundaries.
- **What the AI produced:** It gave me 20 examples (10 first, then I ask for 10 more) that I had to decide myself if a review was "Positive/Recommend" or "Negative/Not Recommend". There were some where I could say it is clearly one or the other but some I wasn't sure about given the combination of both sentiment and behavior/intent to recommend. 
- **What I revised or overrode:** Because of the stress testing, I recognized that combining "Positive"/"Negative" with "Recommend"/"Not Recommend" could be confusing and troublesome, I decide to stick to just the "Positive"/"Negative" sentiment classification of reviews. It's possible for someone to have negative reviews for the game, but still recommend the game because of other aspects of the game. This was the key deciding scenario.
