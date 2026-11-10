# TakeMeter

> ### 👋 Start here
>
> **New to this repo? Read [RUNNING.md](RUNNING.md) first** — setup, the
> notebook, the baseline, and what to do when something breaks.
>
> Once `python test.py` passes:
>
> ```bash
> head -5 data/practice_labels.csv     # the shape your labels.csv needs
> ```
>
> Then open `takemeter.ipynb` **in this folder** — in VS Code, or with
> `jupyter notebook` if you prefer. Pick the kernel: the `.venv` inside this
> project. Run section 1, which reports the hardware you'll be training on.
> Everything else waits until you have data.
>
> Nothing to upload, nothing to connect, no accounts and no keys. The notebook
> runs on your machine and writes next to your code.
>
> **The rest of this file is your submission.** Fill it in as you go.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     HOW TO USE THIS FILE

     Unit 5 asks for the first five sections. Unit 6 adds the five below them.

     Everything is pasted as TEXT. No screenshots, no images.

     ⚠️ The confusion matrix especially. The notebook prints one as a markdown
     table, ready to copy. A screenshot of a matrix earns nothing. Paste the
     table.
     ───────────────────────────────────────────────────────────────────────── -->

<!-- ═══════════════════════ UNIT 5 — THE BUILD ═══════════════════════ -->

## What This Does

<!-- Your community, and what your classifier sorts posts into. Three or four
     sentences. -->

TakeMeter sorts posts from r/movies, a public subreddit that can be read without signing in, into four labels: `analysis`, `hot_take`, `reaction` and `question`. The labels came from what I saw while reading posts, and questions and recommendation requests turned out to be about a quarter of my sample, so the starter's three labels were not enough. No stretch goals planned.

---

## Label Taxonomy

<!-- Each label: a one-sentence definition and two real examples from your
     reading. Then your decision rule for the hardest boundary.

     The decision rule is worth a point on its own and it's the thing most
     people leave out. Every taxonomy has a hardest boundary. Name yours. -->

### `analysis`

**Definition:** Primarily makes a claim whose reasoning depends on specific, checkable details, such as scenes, quotes, dates, or plot events; if removing the details the argument relies on leaves the argument essentially intact, those details do not qualify as support.

**Example 1:**

> Small detail I noticed watching Ghost (1990) yesterday despite it being the 50th viewing
>
> It's likely to be unintentional, but who knows maybe it was a deliberate parallel?
>
> In the beginning, Sam helps out to gather the angel statue from the window by swinging his body like a pendulum to bounce it back.
>
> At the very end, Carl's death is caused by a chain _swinging like a pendulum_ and bouncing _into a window_...

**Example 2:**

> Children of Men (2006) was the first dystopian film I ever really watched. It was set in 2027…
>
> The detail is flawless - London had only won the bid for the 2012 Olympics the year before its release and yet Theo is wearing a London 2012 Olympic jumper in the scene at Jasper's House.
>
> All other futuristic/dystopian films showed a world of technological advance well beyond what was realistic when you look back but not Children of Men.

### `hot_take`

**Definition:** Primarily argues for a judgment or opinion about a movie without an argument that depends on a specific, checkable detail.

**Example 1:**

> Rewatched "In Good Company" with Dennis Quaid, Topher Grace, and a young ScarJo and how enjoyable to watch a movie that uses honest, real life experiences and responses instead of contrived, over the top melodrama.
>
> Rewatching it was such a treat. Its so nice to see a movie so honest and normal. There's no over the top bad guy conniving, or annoying misunderstandings nobody talks about. People say how they feel, and react like real, normal people I have in my life. Scarjo and topher's relationship plays out so honest that its almost unexpected (I'm trying really hard not to spoil it). Quaid plays a football good guy "dad" that never says anything overly smart but clearly is, and leads with good, clean intentions and doing what's right, like a real person we all know. The movie generates different emotions but remains an enjoyable, GOOD film, that never once has you say "like that would happen".

**Example 2:**

> Here Comes The Boom (2012) The perfect family/sports movie?
>
> Here Comes the Boom keeps aging like wine in my rewatches. I had no love for Kevin James before seeing this in 2012 and I've not really followed him after but this one movie really strikes such a great balance of feel-good, action, comedy, and inspiration.
>
> It's of course not a perfect movie and it could be nitpicked to death but in the category of PG family-friendly sports movies I think it might be one of the best.
>
> It has such positive core messaging about..
>
> - Being passionate
> - About inspiring others
> - Not giving up
> - Education
> - The Arts
> - Immigrants
>
> The performances are all very fun, even the non actor MMA people do a good job.
>
> It is genuinely thrilling fight scenes that feel brutal enough to feel real but not so brutal it can be enjoyed by most of the entire family.
>
> Its pacing is good… and come on… best use of a Holly Holy in film.

### `reaction`

**Definition:** Primarily expresses the writer's personal feelings or experience in response to a movie, scene, trailer, or movie-related event.

**Example 1:**

> Rewatched Walter Mitty for the umpteenth time.
>
> I just rewatched The Secret Life of Walter Mitty again for the however many times. So glad I own this one. Such a brilliant feel good movie. Need more movies like this.
>
> Now unfortunately on the soundtrack, the Mitty Mix of Space Oddity is not to be found on any of the streaming services due to some change on licensing rights. Sad!

**Example 2:**

> In The Blink of An Eye
>
> I loved it. The 'expert' reviewers gave it negative reviews. Has any one else seen it and thought, "wow, this is good, I'm am moved by the storyline, I'm going to watch out again" which is me. It is on Disney+ Hulu, not sure if it is on any other streaming services. Just want to know if others felt it was good enough to watch twice or more?

### `question`

**Definition:** Primarily seeks information, explanations, opinions, or recommendations from the community rather than mainly expressing a personal reaction or arguing a position.

**Example 1:**

> movies like prisoners or the whisper man
>
> my favoritee genre right now is movies about serial killers/abduction/mysteries. I just watched the whisper man and really liked that and prisoners is another one i LOVE. I need more movies like these ones- if they dont have the abduction or killer aspect, any dark, psychological, folksy or like suburbia themed horror movie will do.

**Example 2:**

> A Nightmare Before Christmas
>
> Am I the only one curious on what goes on behind the doors that take you to Thanksgiving Land and St. Patrick's Day Land? I mean, Christmas we see. Easter we can figure out. But Thanksgiving Land? Are there people constantly gorging themselves? And in St. Patrick's Day Land, is it one big drunken party?

### The hardest boundary

**Which two labels:** `reaction` vs `hot_take`. Example: the Free Guy post.

> Free Guy
>
> I just took a trip overseas in which I ended up watching a total of 5 movies on the planes that I hadn't seen before, and although Free Guy was probably the best one I watched, I wouldn't say it's great. Although it's rather amusing, especially Ryan Reynolds' performance, I don't think the plot works too well.

It reports a viewing experience and also judges the movie's merits (the plot "doesn't work too well"), so both labels are defensible.

<!-- e.g. "If the post names a specific checkable fact, it's `analysis`, even
     if the tone is heated." -->

**The decision rule I used every time:** Label by the post's primary purpose, not its final sentence. For `analysis` versus `hot_take`, ask whether the argument depends on specific, checkable details. For `reaction` versus `hot_take`, distinguish personal feelings from judgments about the movie; if both remain equally prominent, default to `hot_take`.

**Second boundary, `question` vs `analysis`:** If the body of the post argues from a specific detail and the question is only a closing prompt, label it `analysis`; if the post mainly exists to get an answer, label it `question`.

---

## The Dataset

**Where the posts came from:** r/movies (public, no login), whole text posts copied by hand from the New, Top and Discussion/Question/Recommendation/Review views, one post per row, across many threads. I skipped image-only, link-only and trivia/announcement posts because they fit none of my four labels.

**How I labelled them:** 20 posts were labelled cold (no AI, no tools), marked `cold`. The other 81 rows were pre-labelled by an AI tool using my four definitions; I read every one and could change it, and they are marked `AI-assisted` in the note column.

**Why 101 rows, not 200:** I ran out of fresh r/movies posts (the New view kept repeating) and ran short of time. This is under the 150-row floor; I will add rows during the extension.

**Counts per label:**

| Label     | Count | Share |
| --------- | ----- | ----- |
| question  | 33    | 33%   |
| hot_take  | 32    | 32%   |
| reaction  | 18    | 18%   |
| analysis  | 18    | 18%   |
| **Total** | 101   | 100%  |

**Three hard cases**

**1.**

> _The post:_
>
> > I'm forty-one and just watched True Romance for the first time. Wow!
> >
> > This movie is pure fun, nonstop energy that keeps you invested. I've always enjoyed Christian Slater and felt like he should have been a bigger name, and this has got to be one of his best roles. I never cared for Patricia Arquette too much but she won me over here with her spunky portrayal as Alabama. She is too cool when she faces off against Gandolfini and keeps laughing hysterically despite getting her butt kicked. The comedy and action is gold. The scenes with Gary Oldman as the dreadlocked pimp and Walken and Hopper exchanging insults with eggplants and cantaloupes, are incredible. How many times have you watched this movie?
>
> _Could have been:_ `reaction` or `hot_take`
>
> _I chose `reaction`, because:_ The post primarily expresses the writer's personal enjoyment of the movie, using phrases such as “pure fun” and “keeps you invested.” Although it mentions specific scenes and actors, these details mainly illustrate the writer's enthusiasm rather than support a central argument that depends on them. The closing question invites others to share their viewing experiences, but the post is primarily a personal reaction.

**2.**

> _The post:_
>
> > Demolition (2015)-Question about the start of the movie
> >
> > Trigger warning: Self harm
> > Spoiler for the first 5 minutes of the movie incoming. The event that kicks off the movie is the death of the main character's wife in a car accident. When I watched the scene for the first time I assumed that the wife had crashed the car on purpose and she had successfully killed herself. This was actually the scene that prompted me to watch the movie, I saw it on social media. But after the circumstances surrounding the crash were barely discussed in the movie, I was wondering if the movie's intention was to portray the crash as intentional or as an accident. Maybe I misunderstood.
> > The way the wife looks at the main character while looking away from the road for way too long makes me think she crashed on purpose and was intending on killing herself, perhaps even killing both of them.
>
> _Could have been:_ `analysis` or `question`
>
> _I chose `analysis`, because:_ The writer develops an interpretation of the car crash by pointing to a specific scene detail: the wife looks at her husband while looking away from the road. The writer uses this observation to support the possibility that the crash was intentional. Although the post asks whether this interpretation was correct, the question follows a detail-based argument, so analysis is the better fit under my decision rule.

**3.**

> _The post:_
>
> > Robert Altman's "The Player": Curious commentary on Hollywood with a stellar cast: Yay or nay for you?
> >
> > To be honest, this is one of my least favorite Altman movies. The commentary could have been more biting, Tim Robbins' character was deeply unlikable and not the easiest character to follow. Greta Scacchi was gorgeous in it but it's a thin role. I wish Whoopi Goldberg had a bigger part, they don't really do much with her considering she's the detective on the case.
>
> _Could have been:_ `reaction` or `hot_take`
>
> _I first labelled it `reaction` (cold); on reading I judge `hot_take` because:_ The post primarily argues that the movie is disappointing, criticizing its commentary, the main character, and the limited use of Whoopi Goldberg's character. Although “To be honest” introduces a personal opinion, the post goes beyond expressing a feeling by making several judgments about the movie's quality and specific creative choices. The opinions are the main purpose, rather than a description of the writer's emotional experience, so hot_take is the better fit.

_Note:_ My cold label for this post in `labels.csv` is `reaction`. On rereading under my definitions it is closer to `hot_take`. I left the original cold label unchanged so the cold set stays honest, and it may show up in my consistency check (criterion 4) and my unit 6 diagnosis.

---

## The Training Run

**Base model:** distilbert-base-uncased

**Settings:** 3 epochs, learning rate 2e-5, batch size 16, 128 tokens per post, seed 42. Trained on cpu (Intel Mac, x86_64), torch 2.2.2, 8 GB RAM.

**Anything I changed from the defaults, and why:** Nothing. I used the notebook defaults. I did not retrain or adjust settings after seeing results, because that would be tuning against the test split.

**Split sizes:** train 69 / val 16 / test 16 (101 rows total). Test per label: analysis 3, hot_take 5, reaction 3, question 5. All four labels are under about 8 in test, so I expect scores to jump a lot between seeds.

---

## How I Used AI

<!-- Two specific moments — what you asked, what came back, what you changed.

     ⚠️ Plus disclosure of any pre-labelling. If you had a model pre-label a
     batch and then read and corrected every one, say that. It's an allowed
     workflow and disclosing it costs you nothing. Not disclosing it is the
     problem. -->

**Moment 1**

- _What I asked for:_ I asked an AI to attack my four label definitions: could a second person apply each sentence without guessing? I rewrote them over several rounds.
- _What came back:_ It flagged that "facts or evidence" was a loophole in `analysis` and `hot_take`, because a long review that gives reasons can feel like evidence without containing a checkable fact. It also pointed out that `reaction` was circular and that my tie-break repeated the same question instead of settling it.
- _What I changed:_ I rewrote `analysis` so the argument must depend on specific, checkable details, and added a deletion test (if removing those details leaves the argument intact, they don't count). I made `hot_take` explicitly cover detailed reviews with nothing checkable, and I set the `reaction` vs `hot_take` tie-break to default to `hot_take`.

**Moment 2**

- _What I asked for:_ I asked an AI to write eight posts that sit on the boundaries between my labels, without telling me the intended labels, so I could stress-test the definitions.
- _What came back:_ Eight short posts. I classified them quickly and three didn't match what the AI intended. Two were posts that mention a scene but make no argument from it, and one was an evaluation that sounded personal.
- _What I changed:_ I reread those three against my definitions and decided I had rushed, not that the wording was wrong, so I kept the definitions. It also showed me my boundary rule had no answer for a post that argues from a detail and then asks a question, so I added a second tie-break for `question` vs `analysis`.

**Unit 6, Moment 3**

- _What I asked for:_ I asked an AI to attack my verdict and diagnosis wording for each criterion, and to check whether my claims could be verified from the result files.
- _What came back:_ It pointed out that I had only looked at the seed 42 confusion matrix, so "met on seed 42 only" was not a real verdict, and it suggested reading the other two seeds from `results_three_seeds_before.json`. It also flagged that the zero confusion between `reaction` and `hot_take` on seeds 42 and 2024 only happened because the model never predicted `reaction`.
- _What I changed:_ I printed all three matrices myself and found that seed 7 predicted `hot_take` for all 16 test posts, so criterion 5 was missed, not met. I rewrote the diagnosis to say the passes proved nothing. I also dropped several claims I could not check against the files (for example, that I had been influenced by the staff taxonomy), and I verified every number in my README against the JSON and CSV files before keeping it.

**Pre-labelling disclosure:** 20 rows were labelled cold, with no AI and no tools, and are marked `cold`. The other 81 rows were pre-labelled by an AI tool using my four definitions, with a short reason for each. I read every post and could change any label, and each of these rows is marked `AI-assisted` in the note column. I also used an AI tool to help build the CSV (a short script that writes the rows with correct quoting). In unit 6 an AI tool also helped me spot patterns in my errors (the cold vs AI-assisted split in the relabel, the pair table, and the collapse-to-one-label reading of the matrices); I checked each number against the files.

<!-- ═══════════════════════ UNIT 6 — THE TEST ═══════════════════════

     Don't fill these in during unit 5.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Baseline vs. Trained

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->

| Measure          | Baseline | Trained | Difference |
| ---------------- | -------- | ------- | ---------- |
| Overall accuracy | 0.188    | 0.312   | +0.125     |
| Macro F1         | 0.079    | 0.119   | +0.040     |
| F1 — `analysis`  | 0.000    | 0.000   | +0.000     |
| F1 — `hot_take`  | 0.000    | 0.000   | +0.000     |
| F1 — `question`  | 0.000    | 0.476   | +0.476     |
| F1 — `reaction`  | 0.316    | 0.000   | -0.316     |

**What I predicted before I looked:**

<!-- Milestone 1 asks you to write this BEFORE seeing the trained numbers. A
     prediction made afterwards isn't one. -->

I expect the baseline to do best on `question` because questions often have recognizable wording and a clear purpose. I expect it to do worst on `reaction` because personal reactions can overlap with `hot_take`, making the distinction between expressing feelings and judging a movie more difficult.

**What the gap actually means:**

The trained model scored higher than the baseline, with 31.2% accuracy compared with 18.8%, or approximately 2 additional correctly classified posts out of 16. However, both models performed poorly, and the difference is only one or two posts away from the 25% reference point for four equally likely labels. The trained model received a nonzero F1 score only for `question`, while the baseline received a nonzero F1 score only for `reaction`. The trained model may have predicted `question` frequently rather than learning to distinguish that category reliably. The baseline may also have struggled with the detailed, multi-part label definitions because it was not fine-tuned on my examples. The small training dataset and limited test examples per label (3–5) are additional possible reasons for the weak results, but more evidence is needed to determine their impact.

---

## Run Log — Before

| Criterion                   | Target             | Seed 42     | Seed 7        | Seed 2024   | Verdict            |
| --------------------------- | ------------------ | ----------- | ------------- | ----------- | ------------------ |
| 1. Accuracy per seed        | at least 70%       | 0.312       | 0.312         | 0.375       | MISSED             |
| 2. Every label F1           | at least 0.50 each | see below   | see below     | see below   | MISSED             |
| 3. Largest label share      | at most 50%        | n/a         | n/a           | n/a         | MET (question 33%) |
| 4. Relabel agreement        | at least 18 of 20  | 8 of 20     | n/a           | n/a         | MISSED             |
| 5. reaction called hot_take | at most 50%        | 0 of 3 (0%) | 3 of 3 (100%) | 0 of 3 (0%) | MISSED             |

**Per-label F1 (criterion 2):** order is the label, then seeds 42, 7, 2024.

| Label      | Seed 42 | Seed 7 | Seed 2024 |
| ---------- | ------- | ------ | --------- |
| `analysis` | 0.000   | 0.000  | 0.000     |
| `hot_take` | 0.000   | 0.476  | 0.333     |
| `reaction` | 0.000   | 0.000  | 0.000     |
| `question` | 0.476   | 0.000  | 0.500     |

### Confusion matrix (seed 42)

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

| true \ predicted | analysis | hot_take | reaction | question |
| ---------------- | -------- | -------- | -------- | -------- |
| **analysis**     | 0        | 0        | 0        | 3        |
| **hot_take**     | 0        | 0        | 0        | 5        |
| **reaction**     | 0        | 0        | 0        | 3        |
| **question**     | 0        | 0        | 0        | 5        |

**My biggest off-diagonal number, and what it means:**

<!-- Not "the model made mistakes" — WHICH boundary it didn't learn, and which
     direction. "7 real analysis posts were called hot_take and only 3 went the
     other way" is a direction, not just an error rate. -->

In the seed 42 matrix, the largest off-diagonal count was 5 real `hot_take` posts predicted as `question`, but this reflects the model predicting `question` for all 16 test posts, not a confusion between those two labels in particular.

In seed 7 the model predicted `hot_take` for all 16 test posts, the mirror of seed 42, and in seed 2024 it predicted `question` for 15 of 16 posts. The three seeds collapse onto a single label in different directions.

---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| #   | Criterion                    | Target                                    | Verdict | How I decided                                                                                        |
| --- | ---------------------------- | ----------------------------------------- | ------- | ---------------------------------------------------------------------------------------------------- |
| 1   | Overall accuracy             | at least 70% on every seed                | MISSED  | 0.312, 0.312, 0.375 (seeds 42, 7, 2024); best seed is 0.375                                          |
| 2   | Per-label F1                 | at least 0.50 for every label, every seed | MISSED  | `analysis` and `reaction` were 0.000 on all three seeds; see the per-label table in Run Log - Before |
| 3   | Label balance                | no label above 50% of `labels.csv`        | MET     | largest label is `question` at 33 of 101 (33%)                                                       |
| 4   | Labelling consistency        | at least 18 of 20 on the seed 42 relabel  | MISSED  | 8 of 20 (40%); 11 of 12 disagreements were AI-assisted rows                                          |
| 5   | `reaction` called `hot_take` | at most 50% per seed                      | MISSED  | 0%, 100%, 0% on seeds 42, 7, 2024; fails on seed 7                                                   |

**Diagnoses**

<!-- For each miss: the cause, and how you know. The four common causes are:
     too few examples for a label, a boundary you applied inconsistently, a
     genuinely hard label pair, and a task the model can't reach from this
     much data.

     ⚠️ Use your agreement report as evidence. It is the only instrument you
     have that can tell a LABELLING problem from a MODEL problem, and this
     section is graded on whether you used it that way. -->

**Criterion 1: Missed.** None of the three seeds reached the 70% accuracy target, scoring 0.312, 0.312, and 0.375 for seeds 42, 7, and 2024, respectively. The confusion matrices show that the model largely collapsed toward a single label: seed 42 predicted only `question`, seed 7 only `hot_take`, and seed 2024 predicted `question` for 15 of 16 posts (seed 42's matrix is shown above; the results for seeds 7 and 2024 are recorded in `results_three_seeds_before.json`). These results are close to the 25% chance-level reference for a four-label task and suggest that the model did not reliably distinguish the categories. Training loss barely changed, from approximately 1.36 to 1.35, after only 15 training steps on 69 posts. Seed 2024 briefly reached 0.50 accuracy at epoch 2 before ending at 0.375, suggesting that its performance was also unstable. Criterion 4 adds a second possible cause: 11 of the 15 AI-assisted posts in the relabel sample received different labels on rereading, although this small sample does not establish how representative those disagreements are of the training data. The small training set may have limited the model's ability to learn the distinctions, but these results do not establish whether insufficient data or inconsistent labels contributed more to the failure, or whether either was the sole cause. With only 16 test posts, each post also represents approximately 6.25 percentage points of accuracy.

**Criterion 2: Missed.** The target required every label to achieve an F1 score of at least 0.50 on every seed. Although `question` reached exactly 0.500 on seed 2024, no seed met the target across all four labels. `analysis` and `reaction` had an F1 score of 0.000 on all three seeds because the model never predicted either label. The other two labels scored above zero only on seeds where they were predicted: `hot_take` reached 0.476 on seed 7 and 0.333 on seed 2024, while `question` reached 0.476 on seed 42 and 0.500 on seed 2024. The confusion matrices show the model largely collapsed toward one label on each seed—`question`, `hot_take`, and `question`, respectively—instead of reliably distinguishing all four categories.

The small number of examples may have contributed: `analysis` and `reaction` each had only 18 rows in the dataset and three posts in the test set, so each test post had a substantial effect on their scores. Limited training (69 posts and 15 steps) and possible labeling inconsistencies may also have contributed. Criterion 4 provides relevant evidence for `reaction`: five posts originally labeled `hot_take` were relabeled as `reaction`. Both original `analysis` posts in the relabel sample also received different labels on rereading, although two posts are too few to draw a broader conclusion. These results cannot establish how much data size, limited training, or labeling inconsistency contributed to the failure.

**Criterion 4: Missed.** The target required agreement on at least 18 of 20 posts, but I agreed with my original labels on only 8 of 20 (40%). Of the 12 disagreements, eight moved toward `reaction`, including five originally labeled `hot_take`, two `question`, and one `analysis`. Seven of the 12 disagreements originally had the `hot_take` label, and neither of the two originally labeled `analysis` posts retained its original label. I did not use `analysis` at all on the relabel, which suggests I may have applied the deletion test more strictly than when assigning the original labels. Agreement was also much lower on AI-assisted rows: I agreed with 4 of 15 (26.7%), compared with 4 of 5 (80%) on cold, unaided rows. These patterns suggest possible inconsistencies in applying the distinction between `reaction` and `hot_take`, as well as questions about whether accepting AI-assisted pre-labels affected labeling consistency. Because the tie-break rule defaults to `hot_take` when distinguishing `reaction` from `hot_take`, AI-assisted pre-labels may also have leaned toward `hot_take` by design. Rereading drift may have contributed as well. However, the 20-post sample, particularly the five cold rows, is small, and these results cannot establish that AI assistance caused the lower agreement. The staff agreement result of 29/30 used a different three-label taxonomy, so it does not establish consistency within my four-label system.

**Criterion 5: Missed.** Seed 7 classified all three true `reaction` posts as `hot_take` (100%), while seeds 42 and 2024 never predicted `reaction`. Their passing results (0 of 3) therefore do not demonstrate that the model learned the distinction. The confusion matrices show that each seed collapsed toward a single label rather than reliably separating the categories.

My relabeling exercise provides additional evidence of possible label inconsistency: five of the eight moves toward `reaction` were originally labeled `hot_take`. Overall, I disagreed with 11 of 15 AI-assisted posts, compared with one of five cold posts, although the cold comparison is very small. This is consistent with the missed consistency target in Criterion 4 (8 of 20), but it does not establish that AI assistance caused the disagreements. The 29/30 staff agreement came from a separate three-label dataset and does not resolve consistency in my own four-label data. With only 69 training posts, I cannot determine how much the model's results reflect label inconsistency versus insufficient training data.

---

## Agreement Report

<!-- Your rate against the staff set, and every disagreement adjudicated.

     Remember you labelled these 30 under the STAFF taxonomy in
     data/staff_taxonomy.md, not your own — so every argument below is made
     from those definitions and those decision rules. -->

**Agreement rate:** 29 / 30 = **97%**

<!-- Nobody grades this number. A 60% who argues every disagreement from the
     stated rules beats a 95% who wrote "staff was right" nine times. Several
     of the 30 were chosen because they're genuinely ambiguous — you should be
     winning some of these. -->

I labelled all 30 posts using the staff taxonomy in `data/staff_taxonomy.md` without viewing the staff labels, and committed `my_staff_labels.csv` (commit `e5e7849`) before running `agreement.py` against them.

### Disagreement 1 — sp_010

<!-- Three lines each: the post, both labels, and who you think is right and
     why — grounded in the staff definitions you were both applying.

     Then sort each into one of three piles:
       (a) the rule covered it and I applied it loosely → a consistency problem
       (b) the rule genuinely doesn't say               → a gap in the definitions
       (c) the rule is ambiguous here and my reading is defensible → argue it.
           This is a legitimate win.

     Pile (a) is the one that matters most for your diagnosis: if you applied a
     written rule two different ways on 30 posts, that is direct evidence about
     what you did across your own 200. -->

**1.**

> _The post:_
>
> Three of us ran the same session on the same day, different shoes, within 10 seconds of each other over 5 miles. I'm not saying shoes do nothing, but whatever they do was smaller than the noise between three people.
>
> _Staff said / I said:_
>
> Staff: `analysis` / Me: `hot_take`
>
> _My call, and why:_
>
> Staff was right: `analysis`. Under rule 1, a specific, checkable fact must carry the argument rather than merely decorate an opinion. Here, the comparison between three runners wearing different shoes and finishing within 10 seconds over five miles provides the basis for the conclusion that the effect of the shoes was smaller than the variation between runners. Although three runners are a small sample and do not establish a scientifically conclusive result, the staff taxonomy does not require conclusive proof. The observation still supports the writer's argument, making `analysis` the stronger label. The post also has the same shape as sp_004 (a comparison, what it showed, an inference), with no claim stated first and then decorated.
>
> _Which pile:_
>
> (a) The rule covered this case. I let the weakness of the evidence outweigh the question of whether it carried the argument.

### What the pattern in my disagreements tells me

There was one disagreement out of 30 posts, involving the `analysis` versus `hot_take` boundary. The disagreement shows that I need to distinguish between weak evidence and an unsupported claim. A small sample may limit the strength of a conclusion, but it does not automatically make the evidence decorative or irrelevant to the argument.

The 97% agreement indicates strong consistency with the staff's three-label taxonomy on this particular set. However, it does not establish the consistency of my own four-label TakeMeter dataset, which uses different definitions and a different set of posts.
The same analysis versus hot_take boundary is what my own four-label data turns on, and 81 of my 101 rows were AI pre-labelled, so this miss is a warning about borderline analysis rows. Thirty posts is also a small sample, so 97% could be 90% or 100% on another set.

---

## The Improvement

**What I changed:** I raised the number of training epochs from 3 to 10 in section 2 of the notebook (`EPOCHS = 3` to `EPOCHS = 10`). Nothing else changed: learning rate 2e-5, batch size 16, 128 tokens, the same `labels.csv`, the same 69/16/16 split, and the same three seeds (42, 7, 2024). I set `RUN_LABEL = "after"`, so the results are in `results_three_seeds_after.json` and the before run in `results_three_seeds_before.json` is untouched.

**Which diagnosis pointed at it:** My Criterion 1 and Criterion 2 diagnoses found that every seed collapsed to a single label and that training loss barely moved (about 1.36 to 1.35) after only 15 training steps on 69 posts. That pointed at too little training signal, which more epochs can address without new data. The Criterion 4 result (8 of 20) pointed at label inconsistency as a second possible cause, but I could not fix that within this change, so I chose the training setting as the one change.

### Run Log — After

| Criterion                   | Target             | Seed 42           | Seed 7            | Seed 2024         | Verdict                             |
| --------------------------- | ------------------ | ----------------- | ----------------- | ----------------- | ----------------------------------- |
| 1. Accuracy per seed        | at least 70%       | 0.500             | 0.500             | 0.438             | MISSED                              |
| 2. Every label F1           | at least 0.50 each | 0.000 on 2 labels | 0.000 on 2 labels | 0.000 on 2 labels | MISSED                              |
| 3. Largest label share      | at most 50%        | n/a               | n/a               | n/a               | MET (unchanged, data not changed)   |
| 4. Relabel agreement        | at least 18 of 20  | n/a               | n/a               | n/a               | MISSED (unchanged, not re-measured) |
| 5. reaction called hot_take | at most 50%        | 2 of 3 (67%)      | 2 of 3 (67%)      | 2 of 3 (67%)      | MISSED                              |

### Confusion matrix, after (seed 42)

| true \ predicted | analysis | hot_take | reaction | question |
| ---------------- | -------- | -------- | -------- | -------- |
| **analysis**     | 0        | 1        | 0        | 2        |
| **hot_take**     | 0        | 5        | 0        | 0        |
| **reaction**     | 0        | 2        | 0        | 1        |
| **question**     | 0        | 2        | 0        | 3        |

The model now predicts two labels (`hot_take` and `question`) instead of one. The biggest off-diagonal count is 2, and it occurs three times: true `analysis` called `question`, true `reaction` called `hot_take`, and true `question` called `hot_take`. However, `analysis` and `reaction` were never predicted, so the zeros in their columns are not evidence that those pairs are separable.

**Did it help, and how do I know:**

<!-- If it didn't, say so. Relabelling that didn't help is a genuinely
     interesting result and earns full credit. -->

Partly. Raising the epochs from 3 to 10 improved accuracy on every seed (0.312 to 0.500 on seeds 42 and 7, and 0.375 to 0.438 on seed 2024) and macro F1 rose from 0.119, 0.119 and 0.208 to 0.303, 0.303 and 0.268. The model also stopped collapsing onto a single label: every seed now predicts both `hot_take` and `question`, and each of those two labels reached an F1 of at least 0.50 on every seed (0.545 to 0.667 for `hot_take` and `question`). On seed 2024, validation loss fell from about 1.36 to 1.24 over the 10 epochs, instead of staying flat as in the 3-epoch run, which supports the diagnosis that the 3-epoch run had too little training signal.

It did not change the outcome against my criteria. Criterion 1 is still missed (0.500, 0.500, 0.438 against 0.70) and Criterion 2 is still missed, because `analysis` and `reaction` were never predicted on any seed (F1 0.000). Criterion 5 got worse: 2 of 3 true `reaction` posts were predicted as `hot_take` on all three seeds (67%), so it now fails on every seed instead of one. Criteria 3 and 4 were not re-measured because the data did not change.

I can say that more epochs helped the model learn the two larger labels, but not the two smallest (18 rows each, 3 test posts each). That fits the data-size and label-consistency explanations from my diagnoses, which this change could not test. The caveats are that the test split has only 16 posts (one post is 6.25 points) and each seed was run once, so a 6-point gain on seed 2024 is within one post of no change.

---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped. -->

### Criteria 1 and 2 — Model performance

After increasing the epochs from 3 to 10, accuracy was higher across all three seeds, changing from 0.312/0.312/0.375 to 0.500/0.500/0.438. Two seeds gained three correctly classified test posts, while the third gained one. However, none of the seeds reached the 70% accuracy target. Furthermore, `analysis` and `reaction` remained at 0.000 F1 across all three seeds because the model never predicted either label. The results show that the original single-label collapse was eliminated, but the model still did not successfully classify all four labels.

One possible next step would be to collect more posts, particularly examples of `analysis` and `reaction`, and retrain the model. My Criterion 2 reasoning in `criteria.md` already identified the small number of examples per label as a limitation. I would also consider sampling older posts or other flairs to address the shortage of fresh posts. Adding more examples is a potential improvement, not a proven solution, because they would also need to be labeled consistently and represent the distinctions defined in my criteria. I stopped at this stage because the assignment allowed one improvement, which I used to increase the epochs from 3 to 10. Collecting and labeling more posts would require additional work, and I had already struggled to find enough fresh posts to reach the intended dataset size.

### Criterion 3 — Label distribution

This criterion was met. The largest label represented approximately 33% of `labels.csv`, remaining below the 50% limit. No additional correction was necessary for this criterion.

### Criterion 4 — Labeling consistency

My relabeling agreement was 8/20, well below the target of 18/20. Cold-labeled posts had 4/5 agreement, compared with 4/15 for AI-assisted posts. Cold rows agreed far more often, but only five cold rows were sampled, so this is a pattern rather than a conclusive result. Eight of the twelve disagreements involved a change toward `reaction`, with most of those originally labeled `hot_take`.

A logical next step would be to reread the AI-assisted `hot_take` and `reaction` examples against my existing definitions and tie-break rule, then count how many labels would change if I applied those rules consistently. The results do not establish that AI assistance caused the disagreements, but they identify a pattern worth investigating. I stopped without making those additional labeling changes because they would have constituted another improvement beyond the one I had already made.

### Criterion 5 — Reaction versus hot_take

This criterion was missed because the model never predicted `reaction`. For every seed, 2 of the 3 true `reaction` test posts were predicted as `hot_take`, exceeding the permitted 50%. The remaining true `reaction` post was predicted as `question`. A logical next step would be to add more `reaction` rows and relabel borderline `reaction`/`hot_take` examples using the existing tie-break rule. This issue is related to the classification and labeling difficulties identified in Criteria 1, 2, and 4, although the results do not establish that addressing those issues alone would resolve Criterion 5.

**The gap between what I meant my labels to capture and what the model learned:**

I intended the model to distinguish four labels based on the purpose and characteristics of each post, including reasoning supported by specific, checkable details for `analysis` and personal feelings or experiences for `reaction`. After increasing the epochs to 10, the model predicted only `hot_take` and `question`; the confusion matrices for all three seeds show entirely zero-valued prediction columns for `analysis` and `reaction` (seed 42 is shown above; seeds 7 and 2024 are recorded in `results_three_seeds_after.json`). Given the small test set of 16 posts and the labeling inconsistencies identified during relabeling, I cannot determine whether insufficient training data, inconsistent labels, or the model's ability to learn these distinctions was the main limitation.

<!-- Two sentences. Your confusion matrix is the evidence. -->

<!-- ═════════════════════════════════════════════════════════════════════

     SUBMISSION CHECKLIST — unit 5

       [ ] criteria.md has five numbered criteria, each naming a NUMBER
       [ ] Each has a reason underneath tied to your data or taxonomy
       [ ] labels.csv: at least 150 rows, text/label/note, ONE file not split
       [ ] No label above 70%
       [ ] All five unit 5 sections have real content
       [ ] Label Taxonomy includes the decision rule for your hardest boundary
       [ ] The Dataset includes three hard cases
       [ ] results.json and test_split.csv committed (the notebook does this)
       [ ] At least four new commits
       [ ] Repository URL submitted — WRITE IT DOWN

     SUBMISSION CHECKLIST — unit 6

       [ ] Baseline vs. Trained table, with your prediction written beforehand
       [ ] Run Log — Before, five criteria across three seeds
       [ ] Confusion matrix TYPED AS A MARKDOWN TABLE
       [ ] A verdict on every criterion
       [ ] A diagnosis for every miss, using the agreement report as evidence
       [ ] Agreement Report with every disagreement adjudicated
       [ ] One improvement, with Run Log — After
       [ ] What's Still Broken
       [ ] results_three_seeds_before.json, results_three_seeds_after.json,
           baseline_results.json and
           agreement_results.json committed
       [ ] At least four new commits
       [ ] The SAME repository URL as last unit

     Do not delete and recreate this repository.
     ═════════════════════════════════════════════════════════════════════ -->

---

📖 **How to run this project: [RUNNING.md](RUNNING.md)**
