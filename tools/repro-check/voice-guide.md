# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->

I am a student contributor learning the repository while investigating a specific issue. I want my comments to be clear about what I tested, what I observed, and what I still do not know. Readers should be able to distinguish my evidence from my interpretation.

## Rules I write by

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.

Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->

### Rule: Do not claim more than I know

I state what I actually observed and avoid presenting assumptions or possible causes as confirmed facts.

- Wrong: "The parser is broken because it does not support JavaScript."
- Right: "I reproduced the reported behavior where the skill extractor does not detect JavaScript in this case. I have not yet confirmed the underlying cause."

### Rule: Describe my own investigation

I report the steps and results from my own environment instead of relying on another person's reproduction or saying that I saw the same thing.

- Wrong: "I can confirm this issue too."
- Right: "I tested this on my environment using the steps below and observed the following result."

### Rule: Promise investigation, not a fix

When claiming an issue before reproduction, I say what I plan to investigate and report. I do not promise that I will fix the issue or finish by a specific date.

- Wrong: "I'll fix this bug by the end of the week."
- Right: "I'd like to investigate this issue, attempt to reproduce the reported behavior, and report what I find."

### Rule: Separate evidence from interpretation

I show the relevant output or behavior first, then clearly label any explanation that is still a hypothesis.

- Wrong: "This output proves `_detect_languages` is the problem."
- Right: "This output shows that JavaScript was not detected in this reproduction. `_detect_languages` may be relevant, but I have not confirmed the cause yet."

### Rule: Be specific to the issue

I refer to the actual behavior, environment, and test I am investigating instead of posting generic progress comments.

- Wrong: "I'm working on this issue and will update soon."
- Right: "I'm going to test the reported JavaScript/TypeScript language-detection behavior and will post the environment, reproduction steps, and observed result."

## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->

- A promise to fix the issue before I understand the cause.
- A deadline that I cannot guarantee.
- A claim that I reproduced the bug without evidence showing the reported behavior.
- Another contributor's result presented as if it were my own.
- A guess about the root cause written as a confirmed fact.
- "Same as above" or another piggyback reproduction instead of my own evidence.
