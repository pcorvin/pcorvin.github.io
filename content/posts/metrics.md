+++
title = "LLM benchmarks are not informing their actual performance."
date = 2024-07-28
weight = "20"
meta = "false"
+++

> This is a high-level analysis on current benchmarks for large language models (LLMs) that are developed by OpenAI,
> Anthropic, Mistral et al. Note that I do not have an immediate answer on how to solve this, yet wanted to
> highlight a "devil's advocate" answer to existing cries of LLMs to rule everything.


## Introduction
I am by no means an expert in LLMs, nor foundational models (who truly is?) but I stuck with Deep Learning for quite a bit.
My focus then & now was a bit different, building new,modular network structures with the building blocks available. The famous ["Attention is all you need"](https://arxiv.org/pdf/1706.03762) paper was
interesting when it came out, I personally used the structure for auto-encoder structures in feature abstraction. GPT-2 was also interesting, but
not really worth using, nor at a scale where it mattered.

Aouple of years latter and it escalated. Businesses build on top foundation models & raise gargantuan seed rounds, mostly without looking at
the fundamentals: checking whether it *actually* makes sense to use foundational models.

The main drivers to choose your LLM are benchmarks, which tell you how much better one is relative to the other. People
would rely on an 85.9% MMLU, without any deeper understanding, nor insight.

We thus want to dive into the most common benchmarks, why they do not always (I know, clickbait) reflect on the actual performance
& why you might look beyond the current leader of the LLM Leaderboard.

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

Personal bias led to this selection of these metrics and confirm the hypothesis highlighted at the
beginning. Let us dive into the respective categories:

### Knowledge

MMLU is not good. In fact, the community already developed a successor called [MMLU-Pro](https://arxiv.org/abs/2406.01574), which
inherits parts of the problem. 

MMLU stands for Massive Multitask Language Understanding and should represent a general knowledge database, which aggregates
questions & answers on various topics from different sources. You see the catch.

The benchmark questions contain wrong answers to questions, no answer at all or bad formulation of questions. Furthermore, the split
in topics, their share & what sources are taken into account are not fully documented. If you are interested
in the taxonomy and what can be done better, feel free to access the paper [here](https://arxiv.org/abs/2406.04127).

As mentioned before, Hugging Face & their newest iteration of the LLM leaderboard ([different link than above](https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard))
included MMLU-Pro, which has revisited questions. Despite the efforts of human fact-checking, the question about the sources of answers and their 
systematic checking, remains: How can validate ground truth and how to highlight trusted sources for each subject?

HumanEval suffers from a similar fate, as the coding examples and their narrative are ambiguous.
Most of the examples are too simple to be reflected in complex developer environments (you might have worked with Github Co-Pilot),
where larger code structures pose major problems due to the small context windows.
A new adoption can be driven by [RepoBench](https://github.com/Leolty/repobench), which takes working Github production repositories
as a comparison for auto-completion systems. Performance of LLMs on these remains [low](https://arxiv.org/pdf/2306.03091), especially because of the diversity
of tasks.

### Reasoning

HellaSwag reached saturation, i.e. it is too easy for LLMs to reach near human performance. This clashes with the common
perception of LLMs hallucinating and not grasping Newton's law.

On the contrary, it is mainly due to already shared information datasets or [data leakage](https://www.kaggle.com/code/alexisbcook/data-leakage) happening in trainings. LLMs would
gain access to the validation data during training & prior to the benchmarking process, thus defeating the purpose.GSM-8K is an example for it, which then do not assess the general performance
of the LLM but rather overfitting to the specific data. When tasked  to propose other metrics for reasoning benchmarking, GPT3.5 comes back to HellaSwag as alternative.

The next iteration of reasoning metrics is already in place: [MuSR (Multistep Soft Reasoning)](https://arxiv.org/abs/2310.16049)
is a collection of problems to solve, spanning various topics with varying length. Current performances of LLMs show that
they are at best random in the selection of their answers.


### Math 

Mathematical logic remains a big if for LLMs with several recurring posts about basic operators not being correctly used
& interpreted. MATH remains a solid benchmark & reflects the complexity of math problems in high school. Models do not perform
well in this metric specifically,  as the combination of mathematical statements & plain text becomes more complex to understand.
Current models (Status 07.2024) stick within the low 50s, compared to 80-90s in pure language-based tasks.

In case you are interested in strong mathematical performance, check out [non-LLM deep learning networks](https://deepmind.google/discover/blog/ai-solves-imo-problems-at-silver-medal-level/)
which faired much better under pressure on a higher level.

## Changes & general benchmarking sanity

A benchmark is only as good as its data. And metrics might wear out. Metrics get renewed once a plateau of current
performance can be observed. 

Practical & realistic benchmarks such as RepoBench or the Math Olympiad would be great comparisons, yet might fail to validate
the performance due to the higher complexity. The current times demand a flexible framework given the fast pace at which
models are iterated over and achieve new limits.

Nevertheless, consumers & users should think about their testing suite and what matters most to them. If knowledge bases
is what you are looking for, kindly ignore math & reasoning to fully focus on how good a LLM can retrieve & understand data
through your own RAG infrastructure. If you want to build an AI assistant for children in primary school, math problems might be a major 
factor.

Lastly, do not blindly trust labs publishing the newest results and stressing that their model is the best. Do your
own research and decide what matters most to you and how you can benefit most from what is currently available.

As usual, it depends on your use case.

---
If you are interested in the evolution of LLM comparison, have a look at the Hugging Face blog of the LLM leaderboard.
They do their best to keep the comparison as neutral & up to date as possible with explanations of the changes.

