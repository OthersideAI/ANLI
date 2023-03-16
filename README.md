# Evaluating GPT on the ANLI tasks

In [Language Models are Few-Shot Learners](https://arxiv.org/abs/2005.14165), they got 40% on R3 dev. I'd gotten to 42.5% on it [during the beta](http://gptprompts.wikidot.com/linguistics:anli). Let's see if/how it's improved over time, plus how different methods of hitting turbo with it do.

## Results (On R3 Dev)

| model            | NaiveFewShot | DetailedBreakdown |
| ---------------- | ------------ | ----------------- |
| Original Davinci | 34%          | **34.08%**        |
| Text-Davinci-001 | **34.58%**   | 34.25%            |
| Text-Davinci-002 | **48.33%**   | 40.58%            |
| Text-Davinci-003 | **53.83%**   | 49.08%            |
| Turbo            | **53.75%**   | 50.83%            |
| Turbo-0301       | **54.08%**   | 50.92%            |
| GPT-4            | 66.5         | **69.75%**        |

## Prompts

Here are the prompts. Didn't really do this with a ton of pre-planning, so they're not the most elegant. I'm sure there's a better way to do this that we should come back to again later.

### Naive Few Shot Prompt

The Naive Few Shot Prompt just takes Context A as `Background`, Context B as `Claim`, and then evaliluates the difference between the two.

```
"Background": "The others gave in very soon , and longed to be friends , for now there was no Daisy to pet and cook for them ; no Nan to amuse and doctor them ; and , worst of all , no Mrs. Jo to make home life pleasant and life easy for them .<br>To their great affliction , Mrs. Jo seemed to consider herself one of the offended girls , for she hardly spoke to the outcasts , looked as if she did not see them when she passed , and was always too busy now to attend to their requests .",
"Claim": "Nan was there to doctor them.",
"Part of Claim in Background": "no Nan to amuse and doctor them",
"Evaluation": "In the claim, Nan is there to doctor them. In the background, it is stated that there is no Nan to doctor them. This is inconsistent."
"Verdict": "Contradiction"
```

### Detailed Breakdown Prompt

The Detailed Breakdown Prompt does Context A as `StoryA`, Context B as `StoryB`, then compares them in a bit more detail with an ELI5-style prompt.

```
"StoryA": "The others gave in very soon , and longed to be friends , for now there was no Daisy to pet and cook for them ; no Nan to amuse and doctor them ; and , worst of all , no Mrs. Jo to make home life pleasant and life easy for them .<br>To their great affliction , Mrs. Jo seemed to consider herself one of the offended girls , for she hardly spoke to the outcasts , looked as if she did not see them when she passed , and was always too busy now to attend to their requests .",
"StoryB": "Nan was there to doctor them.",
"Point of Contention": "Nan being a doctor",
"Story A Relevance": "No nan to amuse and doctor them",
"Story B Relevance": "Nan was there to doctor them",
"Explaining the Differences for a Child": "In the first story, 'No Nan to amuse and doctor them' means that there was no one to take care of them. In the second story, 'Nan was there to doctor them' means that Nan was there to take care of them. The first sentence says the opposite of the second sentence.",
"Verdict": "Contradiction"
```
