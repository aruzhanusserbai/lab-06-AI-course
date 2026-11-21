# REPORT — what the measurement showed, who it affects, and whose responsibility it is

## 1. Measurement read-out

**Counts, direction and score shift per attribute** (40 pairs per group).

| attribute | pairs | flips | direction | signed score shift [95% CI] | pairs with different scores | mean abs diff [95% CI] |
|---|---|---|---|---|---|---|
| name_language | 40 | 2 (5.0% [1.4%, 16.5%]) | kazakh favoured 2/0 (p = 0.500); russian 0/1, english 0/1 (p = 1.000) | kazakh +0.7 [−1.8, +3.8], russian +0.2 [−1.7, +2.1], english −1.0 [−4.2, +1.9] | 11/40 | 3.12 [1.38, 5.25] |
| gender_coded_name | 40 | 4 (10.0% [4.0%, 23.1%]) | female favoured 4/0 (McNemar p = 0.125) | male − female −0.4 [−1.2, +0.6] | 6/40 | 1.12 [0.25, 2.13] |
| university | 40 | 1 (2.5% [0.4%, 12.9%]) | flagship favoured 1/0 (p = 1.000) | flagship − regional **+2.5 [+1.1, +4.1]**, sign p = 0.002 | 10/40 | 2.50 [1.12, 4.12] |
| null_name (floor) | 40 | 0 (0.0% [0.0%, 8.8%]) | — | — | 7/40 | 2.00 [0.62, 3.62] |
| null_university (floor) | 40 | 1 (2.5% [0.4%, 12.9%]) | — | — | 9/40 | 2.12 [0.88, 3.62] |

The bare agent shortlisted 356 of 400 profiles (89%) and gave both decisions at score 45 (max reject 45, min shortlist 45); 0 of 400 replies were unparseable.

**Which attribute moved the decision, read against its floor.** None of them. Flip intervals of all three attributes overlap with their floor intervals, and mean absolute score differences overlap too. So I can say that this run doesn't give any evidence that name language, gender coding or university changed who was shortlisted. But I can't say that they have no effect, and if I call a difference that doesn't exceed its floor an "effect" it will be claim that is not supported. The only result that stands out is on the score, not on the decision: applicants from flagship universities got +2.5 [+1.1, +4.1] points higher than same applicants from regional ones. It is the only signed shift whose interval excludes zero. Its size is similar to the floor (mean abs diff 2.50 vs 2.12), but in the floor the sign of difference is random, and here it went the same way in all pairs where scores were different (sign p = 0.002).

**How much could be noise, and what the floors leave untested.** Floors swap one name (or university) for another one of the same kind and everything else stays same, also the layout of the prompt. They moved scores (7/40 and 9/40 pairs), but almost never moved the decision (0/40 and 1/40). They don't test other irrelevant changes. But the optional order probe tested it: 40 pairs of identical applicants, where second one is shown with same lines in other order, gave 10/40 flips = 25.0% [14.2%, 40.2%], and all of them in one direction (McNemar p = 0.002), and mean score was 6.6 [3.5, 9.9] points lower in the other order. Its interval doesn't overlap with null_name floor, so just the layout of the prompt moved desicions more than any protected attribute did. In Part 3 when I removed two lines it changed 166 of 400 scores by 14.01 points on average. So floors understate the noise, and "no attribute exceeds its floor" is true only for this layout. For stronger estimate it will need several hundred pairs per attribute, and floors should be measured with several prompt wordings and field orders.

**What n = 40 could and could not detect.** Exact two-sided McNemar test at 0.05 needs at least 6 one-sided discordant pairs out of 40 (15%) if there is none in other way, 8 if there is one, and 10 if there is two. Gender result (4 vs 0) is below that: direction is consistant, but it can't be distinguished from chance. Score shifts that are smaller than interval half-widths (±0.9 for gender up to ±3.1 for english names) couldn't be told from zero. If real effect is smaller than this I would not see it in my run, so "no measured effect" doesn't mean "no effect".

**Would it hold with another prompt, another model or real applicants?** My run can't support that. Order probe shows that model desicions depend a lot on the form of the prompt, so other wording could change both attribute effects and the floors. Also my run uses only one small model, synthetic applicants who are different in exactly one field, and names and universities from fixed list. Real applicants are different in many fields at once and they come from institutions that model never saw.

**Against my predictions.** I predicted about 15 unparseable replies (actual 0); about 8 university flips with flagship favoured (direction was right, but it was on scores, with only 1 flip); no direction for gender (there was 4 flips, all favouring female names, but it is not established); and that kazakh names will do worst (not supported: shortlisted 96.4% kazakh, 96.2% english, 92.3% russian).

## 2. Who is affected
**Who is on each side of a wrong decision.** Wrongly rejected applicant is someone that agent turns down, even though identical applicant would pass. From measurement I think it is most likely applicants near score 45, cause there bare agent gave both decisions at the same score. The gender flips came with small score differences (mean abs diff 1.12), which fits borderline cases, and all 4 went against male-coded name. It is not established (p = 0.125), but if it is real, then male-coded applicants near the boundary are the ones who are wrongly rejected. Wrongly *shortlisted* applicant doesn't lose anything. Bare agent shortlisted 356 of 400 (89%), so shortlist barely separates applicants, and if places are limited the next stage will rank them by score. And there measured effect matters: regional-university applicant gets 2.5 [1.1, 4.1] points less than identical flagship one, so flagship applicant can be ranked higher than equal regional one and take his place.

**What each wrong decision costs.** Wrong reject costs applicant the scholarship money, maybe even the place at university if he can't pay without it, and a year. And nothing tells him that it was machine who decided or that he can object. Wrong shortlist doesn't cost anything for shortlisted person, its cost goes to the person who was displaced and to reviewers who read the case. So these two errors are not symetric: one is paid by the person that was decided about, and other one by someone who never sees why. Also there was two more costs from Part 4. Bare pipeline turned missing consent and age 17 into rejections, so applicant who only asked to not be processed automatically, or minor, was just rejected instead of being handled by a person.

**Parties the brief does not mention.**
- *Reviewers:* with my harness 58 of 400 applications (14.5%) went to a person, and all of them were rejects. Reviewer who sees model score may just confirm it.
- *The fund:* it has legal responsability for automated decision and also reputational cost if decision is unfair.
- *People who never applied* cause they expected that algorithm will reject them, for example students from regional institutions.
- *Applicants from institutions that model never saw:* model knows university only by its name ("National", "Research" vs "Provincial", "Teachers'"), and I think it is plausible reason of flagship score advantage.
- *Applicants with unusual names or programmes:* my refusal rule refused 0 of 400 generated applicants, but real programme like "Information Systems" or name with unusual character could be refused, and I didn't test it.

**Who bears the cost of what my sample could not detect.** On decisions nothing exceeded its floor, but n = 40 can't detect decision effect that is below 6 one-sided pairs (15%). If gender pattern (4 vs 0) is real effect of about 10%, my run couldn't confirm it, and people who would pay for it are male-coded applicants near the boundary. Same is for any name-language effect that is smaller than about 3 score points. Order probe showed bigger risk that my floors didn't cover: just the order of the lines tipped 10 of 40 identical applicants out of the shortlist. And this cost goes to whoever is near the boundary, it doesn't matter what is their name or university.

**What compounds over time or downstream.** University and order effects are systematic, not random: they push in the same direction for every applicant, every year if the same configuration is used. If score is passed to later ranking, another fund or published list, 2.5-point or 6.6-point shift becomes fixed advantage that nobody checks again. And if the fund later tunes or trains on its own past desicions, the shift goes back into the data, so if there is less regional applicants in the shortlist this year, there will be less examples of successful regional applicants next year.


## 3. Professional responsibility

**My specific responsibilities as the developer, given what I measured.**
- *What I must check before it runs:* matched pairs against their floors, and also layout test, cause just the order of the lines tipped 10 of 40 identical applicants out of the shortlist. Also I must check that escalation band still catches anyone after any change: after blinding my band (40, 45) caught 0 profiles, and all 58 escalations came from the rule that every reject goes to a person. In the counterfactual extension, where model saw names again, the same band caught 2 of 16.
- *What I must tell the people who deploy it:*
  - score is unstable: when I removed two lines it changed 166 of 400 scores by 14.01 points on average, and when I changed only the line order mean score was 6.6 points lower, so score shouldn't be used to rank shortlisted applicants;
  - model "reason" is not explanation: it called entrance exam of 60/140 (the lowest value in the data) "average", and in the log it gave "consent to processing" as a reason;
  - in Part 4 when I changed only the age to 17 shortlist turned into reject, so desicion can move with age, and I didn't hide it and didn't measure it;
  - with n = 40 effect that is below 15% of pairs is invisible.
- *What I must not claim:* that the system is fair; that blinding removed bias (the "after" flips are 0 just by construction, cause both members of pair are shown identical text); or that "no effect beyond the floor" means that there is no effect.

**What discharging them requires, what I have done and what is left.**

| responsibility | what it requires in practice | status |
|---|---|---|
| know if protected attributes move decisions | matched pairs read against floors | done: 200 pairs, none beyond its floor |
| keep decisions independent from prompt form | one fixed and documented field order; order probe re-run after every change | measured (10/40 flips); fixing and documenting the order is left |
| no applicant rejected just by machine | rule: every reject goes to a person | done: 0 automatic rejects (bare: 44) |
| refuse what must not be processed | refusal path for purpose, minors, consent, impossible values, instructions in free text | done: 5 of 6 refused in Part 4, 0 wrong refusals of 400 |
| every decision can be audited | one log record per call | done: 406 records; but tamper-evident storage and reviewer final decision are not logged |
| band that actually works | recalibrate the band on scores of configuration that is used | left: band caught 0 after blinding |
| know effect of age and consent | matched pairs on age; hide or test consent | left |
| a **stop condition** | do not deploy, or stop, if any attribute flip interval clears its floor, if unparseable reply is not escalated, or if band catches 0 after change | defined here, but not automated |

**What belongs to the institution, not to me.**
- Defining the purpose.
- Telling applicants that AI system screens them and that they can object (Law of the RK No. 94-V "On Personal Data and Their Protection", Art. 19-1(2)–(3); Law of the RK No. 230-VIII "On Artificial Intelligence", Art. 7(2)).
- Running manual route for minors and for applicants who don't consent.
- Choosing, training and staffing the reviewers.
- Handling objections in three working days (Art. 19-1(3)).
- Deciding how long log is kept and who can read it.
- Deciding if model is fit for this purpose at all, cause of the order effect.

**Where the two conflict.** Let's say fund wants to drop the rule that every reject goes to a person, cause reviewers cost money. I measured what this rule prevents:
- without it 58 applicants would be rejected just by machine;
- 19 of them was shortlisted by the same model when it saw two more lines;
- model desicions flip with the order of the lines.

My responsibility is to show these numbers to the fund in writing, and also legal requirement behind the rule (Art. 19-1). If fund removes this control anyway, it is fund decision, but then I must not describe the system like it has human oversight of rejections, and I would document that control was removed against my recomendation.

