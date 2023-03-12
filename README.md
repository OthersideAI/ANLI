# Evaluating GPT on the ANLI tasks

In [Language Models are Few-Shot Learners](https://arxiv.org/abs/2005.14165), they got 40% on R3 dev. I'd gotten to 42.5% on it [during the beta](http://gptprompts.wikidot.com/linguistics:anli). Let's see if/how it's improved over time, plus how different methods of hitting turbo with it do.

## Results (On R3 Dev)

| model            | NaiveFewShot |
| ---------------- | ------------ |
| Original Davinci | 34%          |
| Text-Davinci-001 | 34.58%       |
| Text-Davinci-002 | 48.33%       |
| Text-Davinci-003 | 53.83%       |
| Turbo            |              |
| Turbo-0301       |              |
