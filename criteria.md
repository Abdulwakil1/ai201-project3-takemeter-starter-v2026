# Acceptance criteria — TakeMeter

Five criteria that say what "working" means for this classifier, written in
unit 5 **before** anything was trained.

**All five are yours this time.** None are given. You've had two projects of
practice.

An acceptance criterion names a number. _"The model is accurate"_ is an
opinion. _"Every label has an F1 of at least 0.60 on the held-out set"_ is a
criterion.

Under each, write a sentence or two on **why that number**. A reason that says
something about your data or your taxonomy earns credit — _"I picked 0.60 F1
for `reaction` because it's my smallest label and I only have about 50
examples of it"_. A reason that could be attached to any project does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## Pick numbers you can defend

Not numbers that sound impressive. Three labels means a coin-flip guesser gets
about 33%, so a target of 0.40 is barely a target. Your number should sit
somewhere you'd honestly call useful.

**Cover at least three of these five areas.** They're here as prompts, not as a
form to fill in — a criterion that fits none of them is fine if it names a
number.

| Area                  | A question it could answer                                            |
| --------------------- | --------------------------------------------------------------------- |
| Overall accuracy      | How often does it need to be right to be worth using?                 |
| Per-label performance | Is one label allowed to be much worse than the others?                |
| Balance               | How lopsided can your label counts get before it's a problem?         |
| Consistency           | If someone else labelled the same posts, how often should you agree?  |
| Confidence            | Should a confident prediction be right more often than an unsure one? |

Two things worth knowing before you pick numbers, because both will affect
whether you hit them:

- **Your smallest label will have the jumpiest score.** If a label has 50
  examples, about 8 land in the test split. An F1 computed on 8 examples moves
  a lot between seeds. A target for that label should be looser than one for
  your biggest label, and saying so is a good reason.
- **Unit 6 tests across three seeds, and the target has to hold across all
  three.** A target of 0.65 against results of 0.71, 0.62, 0.68 is a **miss**.
  Pick with that in mind — it is stricter than it first sounds.

---

<!-- Your criterion. It must name a number. -->

## 1. Overall accuracy

The classifier must achieve at least 70% accuracy on the held-out test set for each of the three random seeds.

**Why this target:** With four labels, a uniform random guesser would average about 25% accuracy. In my sample, `hot_take` accounted for approximately 36% of posts, so a classifier that always predicts `hot_take` could achieve roughly 36% accuracy. My 70% target requires substantially better performance. The test set has only about 30 posts, so results may vary considerably across seeds.

---

## 2. Per-label performance

Each of the four labels must achieve an F1 score of at least 0.50 on the held-out test set for each of the three random seeds.

**Why this target:** Overall accuracy can hide poor performance on an individual label. I expect `analysis` to be one of the smallest categories because its definition requires reasoning supported by specific, checkable details. If only around 5-8 `analysis` posts appear in a test split, a single error could substantially affect its F1 score. The threshold is intended to require meaningful performance across all labels while recognizing that small test counts make the measurement noisy.

---

## 3. Label balance

No label may account for more than 50% of the labeled rows in `labels.csv`.

**Why this target:** In my observed sample, `hot_take` accounted for approximately 36% of posts. My decision rule also defaults to `hot_take` when `reaction` and `hot_take` are equally prominent. The 50% threshold is stricter than the project's 70% maximum and is intended to prevent one label from dominating the dataset.

---

## 4. Labeling consistency

When I relabel 20 posts selected from `labels.csv` using random seed 42, without viewing their original labels, I must agree with my original labels on at least 18 out of 20 posts (90%).

**Why this target:** This checks whether I can consistently apply my label definitions and decision rules when labeling the same posts again. I will select the posts reproducibly using random seed 42, hide their original labels during relabeling, and compare my new labels with the originals. This measures my own repeatability; the Unit 6 staff-agreement check provides a separate comparison with another person's judgments.

---

## 5. Confusion between `reaction` and `hot_take`

For each of the three random seeds, no more than 50% of posts whose true label is `reaction` may be incorrectly predicted as `hot_take` on the held-out test set.

**Why this target:** My hardest labeling boundary is `reaction` versus `hot_take`, because a post can express personal feelings while also judging a movie's quality. I chose 50% as the maximum acceptable error rate because I want at least half of true `reaction` posts to avoid being misclassified as `hot_take`.However, I recognize that the test set is small: if `reaction` accounts for about 18% of my 200 posts, I expect only about 5–6 true `reaction` posts in the test set. One misclassification could change the error rate by approximately 17–20 percentage points. If a seed's test set contains no true `reaction` posts, this criterion is not evaluable for that seed and will be reported as such, not counted as a pass.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 6 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath, like this:

         ## 2. Every label performs acceptably

         The model performs well on all labels.

         **Why this target:** ...

         > **Revised in unit 6:** Every label has an F1 of at least 0.60 on
         > the held-out set.
         >
         > **Why revised:** "performs well" gave me nothing to check. I
         > couldn't produce a verdict from it at all.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "Overall accuracy of at least 0.65" → "at least 0.55", because
            0.65 turned out to be optimistic for 200 examples.

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.
     ───────────────────────────────────────────────────────────────────────── -->
