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

**Pre-labelling disclosure:** 20 rows were labelled cold, with no AI and no tools, and are marked `cold`. The other 81 rows were pre-labelled by an AI tool using my four definitions, with a short reason for each. I read every post and could change any label, and each of these rows is marked `AI-assisted` in the note column. I also used an AI tool to help build the CSV (a short script that writes the rows with correct quoting).

<!-- ═══════════════════════ UNIT 6 — THE TEST ═══════════════════════

     Don't fill these in during unit 5.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Baseline vs. Trained

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->

| Measure          | Baseline | Trained | Difference |
| ---------------- | -------- | ------- | ---------- |
| Overall accuracy |          |         |            |
| Macro F1         |          |         |            |
| F1 — `label_one` |          |         |            |
| F1 — `label_two` |          |         |            |

**What I predicted before I looked:**

<!-- Milestone 1 asks you to write this BEFORE seeing the trained numbers. A
     prediction made afterwards isn't one. -->

**What the gap actually means:**

<!-- If the baseline matched your trained model, your fine-tuning added
     nothing — and that is a real finding, not a failure. Say it plainly. -->

---

## Run Log — Before

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
| --------- | ------ | ------- | ------ | --------- | ------- |
| 1.        |        |         |        |           |         |
| 2.        |        |         |        |           |         |
| 3.        |        |         |        |           |         |
| 4.        |        |         |        |           |         |
| 5.        |        |         |        |           |         |

### Confusion matrix

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

| true \ predicted |     |     |     |
| ---------------- | --- | --- | --- |
| \*\*\*\*         |     |     |     |
| \*\*\*\*         |     |     |     |
| \*\*\*\*         |     |     |     |

**My biggest off-diagonal number, and what it means:**

<!-- Not "the model made mistakes" — WHICH boundary it didn't learn, and which
     direction. "7 real analysis posts were called hot_take and only 3 went the
     other way" is a direction, not just an error rate. -->

---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| #   | Criterion | Target | Verdict | How I decided |
| --- | --------- | ------ | ------- | ------------- |
| 1   |           |        |         |               |
| 2   |           |        |         |               |
| 3   |           |        |         |               |
| 4   |           |        |         |               |
| 5   |           |        |         |               |

**Diagnoses**

<!-- For each miss: the cause, and how you know. The four common causes are:
     too few examples for a label, a boundary you applied inconsistently, a
     genuinely hard label pair, and a task the model can't reach from this
     much data.

     ⚠️ Use your agreement report as evidence. It is the only instrument you
     have that can tell a LABELLING problem from a MODEL problem, and this
     section is graded on whether you used it that way. -->

---

## Agreement Report

<!-- Your rate against the staff set, and every disagreement adjudicated.

     Remember you labelled these 30 under the STAFF taxonomy in
     data/staff_taxonomy.md, not your own — so every argument below is made
     from those definitions and those decision rules. -->

**Agreement rate:** **_ / 30 = _**%

<!-- Nobody grades this number. A 60% who argues every disagreement from the
     stated rules beats a 95% who wrote "staff was right" nine times. Several
     of the 30 were chosen because they're genuinely ambiguous — you should be
     winning some of these. -->

**Disagreements**

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
> _Staff said / I said:_
>
> _My call, and why:_
>
> _Which pile:_

**2.**

> _The post:_
>
> _Staff said / I said:_
>
> _My call, and why:_
>
> _Which pile:_

**What the pattern in my disagreements tells me:**

---

## The Improvement

**What I changed:**

**Which diagnosis pointed at it:**

### Run Log — After

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
| --------- | ------ | ------- | ------ | --------- | ------- |
| 1.        |        |         |        |           |         |
| 2.        |        |         |        |           |         |
| 3.        |        |         |        |           |         |
| 4.        |        |         |        |           |         |
| 5.        |        |         |        |           |         |

**Did it help, and how do I know:**

<!-- If it didn't, say so. Relabelling that didn't help is a genuinely
     interesting result and earns full credit. -->

---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped. -->

**The gap between what I meant my labels to capture and what the model
learned:**

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
