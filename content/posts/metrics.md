+++
title = "LLM benchmarks are not informing their actual performance."
date = 2024-07-28
weight = "20"
meta = "false"
+++

> This is a high-level analysis on current benchmarks for large language models (LLMs) that are developed by OpenAI,
> Athropic, Mistral et al. Note that I do not have an immediate answer on how to solve this, yet wanted to
> highlight a "devil's advocate" answer to existing cries of LLMs to rule everything.


## Introduction
I am by no means an expert in LLMs, nor foundational models (who truly is?) but I somewhat stuck with Deep Learning for quite a bit,
although the focus back then & now was a bit different. The famous ["Attention is all you need"](https://arxiv.org/pdf/1706.03762) paper was
interesting when it came out, especially for auto-encoder structures in feature abstraction and that was basically it. GPT-2 was also interesting, but
not really worth using, nor at a scale where it mattered.

Couple of years latter and boom, it escalated. Business rely on foundations models & raise gargantuan seed rounds, mostly without looking at
the fundamentals checking whether it *actually* makes sense to use foundational models.

One of the main drivers to choose your LLM are benchmarks, which tell you how much better one is relative to the other. People
would rely on a 85.9% MMLU with most of them not knowing what is actually means. 

We thus want to dive into the most common benchmarks, why they do not always (I know, clickbait) reflect on the actual performance
& why you should not always take the overall leader of the LLM Leaderboard.

## What are the main benchmarks?

You might have checked in on the [Hugging Face LLM leaderboard](https://huggingface.co/spaces/open-llm-leaderboard-old/open_llm_leaderboard), which
represents the industry standard for comparison of LLMs. To have a more complete picture, a sample of SoA metrics will 
be represented by this bunch with their category highlighted in *italic*:

* [MMLU](https://paperswithcode.com/dataset/mmlu) - *knowledge* - Multitask accuracy
* [HellaSwag](https://rowanzellers.com/hellaswag/) - *reasoning* - Understanding situations
* [HumanEval](https://github.com/openai/human-eval) - *knowledge* - Python coding tasks
* [GSM-8K](https://github.com/openai/grade-school-math) - *math/reasoning* - Grade school math
* [MATH](https://arxiv.org/abs/2103.03874) - *math* - Math problems with 7 difficulty levels

Note that these metrics represent their respective category, although you might highlight a missing metric or
that some of these are outdated already: bear with me.

## What is wrong with them?

Of course I selected some metrics which would benefit the cause and are confirming the initial thesis highlighted at the
beginning. Let us dive into the respective categories

### Knowledge

MMLU is not good. Plain and simple, effectively bad that the community already developed a successor called [MMLU-Pro](https://arxiv.org/abs/2406.01574), which
inherits parts of the problem. 

MMLU stands for Massive Multitask Language Understanding and should represent a general knowledge database, which aggregates
questions & answers on various topics from different sources. You see the catch.

The benchmark questions contain wrong answers to questions, no answer at all or bad formulation of questions. Furthermore, the split
in topics, their share & what sources are taken into account are not fully documented. If you are interested
in the taxonomy and what can be done better, feel free to access the paper [here](https://arxiv.org/abs/2406.04127).

As mentioned before, Hugging Face & their newest iteration of the LLM leaderboard ([different link than above](https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard))
included MMLU-Pro, which has revisited questions but nevertheless leaves open questions on the sources of answers and check 
systematically, which of them are correct.

HumanEval suffers from the same fate, as the coding examples and their narrative are ambiguous with
most of the examples are too simple to be reflected in complex developer environment (hello Co-Pilot!).
A new adoption can be driven by [RepoBench](https://github.com/Leolty/repobench), which takes working Github production repositories
as comparison for auto-completion systems. Performance of LLMs on these remains low, especially because of the diversity
of tasks.

### Reasoning

HellaSwag reaches saturation. It is too easy for LLMs to reach near human performance. Are they as good as humans?

Not really, it is mainly due to most of the information being shared in datasets already or leakages happening in trainings.
This effectively is too easy for models having access to more data and inference with web crawling services. Looking for
other metrics to take into account, Claude & GPT4o repeatedly proposed HellaSwag as alternative.

On the other hand, [data leakage](https://www.kaggle.com/code/alexisbcook/data-leakage) becomes increasingly common, where  models were possibly trained on benchmark data or 
on data very similar to benchmark data. GSM-8K is an example for it, which then do not assess the general performance
of the LLM but rather overfitting to the specific data.

### Math 

Mathematical logic remains a big if for LLMs with a number of recurring posts about basic operators not being correctly used
& interpreted. MATH does a great job at this & reflects the complexity of math problems in high school. Models do not perform
well in this metric specifically,  as the combination of mathematical formula & plain text becomes more complex to understand.
Current models (Status 07.2024) stick within the low 50s, compared to 80-90s in pure language-based tasks.

In case you are interested in strong mathematical performance, check out [non-LLM deep learning networks](https://deepmind.google/discover/blog/ai-solves-imo-problems-at-silver-medal-level/)
which faired much better under pressure on a higher level.

## Changes & general benchmarking sanity

A benchmark is only as good as its data. And metrics might wear out. Metrics get renewed once a plateauing of current
performance can be observed. Nevertheless, this opens up the question what the actual benchmark should be.

Practical & realistic benchmarks such as RepoBench or the Math Olympiad would be great comparisons, yet might fail to validate
the performance due to the higher complexity. The current times demand a flexible framework given the fast pace at which
models are iterated over and achieve new limits.

Nevertheless, consumers & users should think about their testing suite and what matters most to them. If knowledge bases
is what you are looking for, kindly ignore math & reasoning to fully focus on how good a LLM can retrieve & undertand data
through your own RAG infra. If you want to build an AI assistant for childern in primary school, math problems might be a major 
factor.

Essentially, do not blindly trust labs publishing the newest results and stressing that their model is the best. Do your
own research and decide what matters most to you and how you can benefit most from what is currently available.

As usual, it depends on your use case.

---
If you are interested in the evolution of LLM comparison, have a look at the Hugging Face blog of the LLM leaderboard.
They do their best to keep the comparison as neutral & up to date as possible with explanations on the changes.

