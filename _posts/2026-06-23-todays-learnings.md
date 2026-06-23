---
layout: post
title: "Today's learnings"
date: 2026-06-23
category: note
tags: [research, reasoning, productivity]
---

## How to be an AI researcher

*Youtube Video: [How to be an AI researcher](https://youtu.be/R-_Ra1z4Bn4)*

This podcast was a turning point for me. It brought me so many realizations because the answers felt very relatable to my situation.

Dr. Vidi is a researcher at the Broad Institute of MIT and Harvard. She did her PhD at Cambridge in probabilistic machine learning. Before research, she worked at Citadel and other quant firms for four and a half years. Her journey from quant finance to AI research is inspiring because it shows that pivoting is possible even when you are deep into one career.

When Harnoor asks about how to start as an AI researcher, her reply was the thing I liked the most. She said to start sharing your learnings. It does not matter if the topic is already covered by many others. It does not matter if nobody sees it. She emphasizes this point strongly:

> *"People who do things when there is no incentive for them will be provided a platform, since they will do it anyway."*

This stuck with me. The idea is that you do not wait for the right time or the right opportunity. You just start. You build evidence that you are already on the curve. When someone later, maybe during a Masters admission or a job interview, wants to know about you, they can see your work and your thinking through your blogs and projects.

She also shared practical advice for undergrads who want to get into research:

- Research papers can feel overwhelming because they are written for a specialized audience. Instead of starting with papers, build side projects. If possible, find people with similar interests and work together.
- More important than anything else is to share your learnings in the form of passages or articles. People often think, "Who cares about my learnings?" But you have to put things out anyway.
- When an opportunity comes and people look at your profile, they will see that you have been doing this for a long time. They will know you will do it with or without them.
- Do not care about how original your learning or ideas are. Just put things out in the world. Maybe nobody will notice. That should not matter.
- Research does not progress every day. Most days, research is failure. What matters is patience and learning from it.

The full interview: [How to be an AI researcher](https://youtu.be/R-_Ra1z4Bn4)

---

## Subbarao Kambhampati

*X profile: [@rao2z](https://x.com/rao2z)*
*YouTube: [Subbarao Kambhampati](https://www.youtube.com/@subbarao2z2/playlists)*

Professor at Arizona State University. Yann LeCun reposted a tweet of his, which is how I found him and his YouTube channel.

I was really proud to learn he is a Telugu person, like me. I also had a friend at IIITH named Advaith Kambhampati. Maybe I will watch some of his videos when I have free time. His work on AI planning and reasoning, especially his paper on chain-of-thought, directly connects to the next section.

---

## Escaping the chain-of-thought trap

*Blog link: [Escaping the chain-of-thought trap](https://bdtechtalks.substack.com/p/escaping-the-chain-of-thought-trap)*

Chain-of-thought (CoT) is a method where the model "thinks step-by-step" before answering. It shows its reasoning in text, step by step, and generates intermediate "thinking" tokens. Now most companies are burning their compute on CoT prompting and training.

Initially, CoT was a great hack. It let us read the trace of what the model was thinking without going through difficult architectural changes. But it increases inference-time compute significantly.

Generating intermediate thinking tokens does not mean cognitive reasoning. There is a quote from the post that I want to remember:

> *"The text bottleneck is bankrupting corporate AI budgets, slowing down inference speeds, and masking the true nature of machine computation. To scale AI sustainably, the industry needs to move beyond the CoT tokens and to alternative reasoning mechanisms."*

The reality is harsh. When an LLM shows its intermediate thinking tokens, we think it is reaching a conclusion. But a paper by Subbarao Kambhampati proves this is wrong.

CoT is an imitation of reasoning. The model can flawlessly explain its steps. But since the previous tokens determine the next tokens, if one step goes away from the correct reasoning path, the model will confidently generate perfectly logical steps but arrive at wrong final answers. The text it generates and the actual computation happening inside are decoupled.

A few more problems with CoT:

- Instead of teaching the model to generalize well for other examples, CoT generates more prompt-specific behaviors that go wrong in long reasoning chains.
- Some cases show that forcing CoT answers reduces accuracy compared to direct answers.
- Long reasoning chains increase memory, compute, and inference costs. They also fill the context window with unnecessary jargon.

The alternative that researchers are exploring is reasoning models with **latent space**. Instead of converting vectors to text at every intermediate step, the model keeps computation inside hidden vector states. Meta's Coconut paradigm and Sapient Intelligence's HRM model are examples of this approach. They process complex logic at speeds unachievable by standard LLMs because they avoid the autoregressive text-decoding bottleneck.

---

## How to approach research in AI

*Blog link: [How to approach research in AI](https://letters.lossfunk.com/p/how-to-approach-research-in-ai)*

This blog by Paras Chopra (founder of Lossfunk) has some other resources attached to it that I need to go through and understand later. The core advice is simple but powerful.

He recommends that every research intern should think and write down:

1. What **research question** are you exploring?
2. A couple of **research hypotheses** accompanying them.

A research hypothesis is your hunch about what is true about the research question. Only once you have hypotheses should you think of experiments that will prove or disprove them.

His warning: Without this structure, you will simply shoot in the dark randomly. That is fine for initial exploration, but eventually you need to methodically explore your research question.

He also says that when running experiments, make sure you know what the core experiment is and what is peripheral. Focus on the core and make simplifying assumptions about everything else. If you do not do that, you will conflate multiple factors and never know why something works or does not work.

---

## Ur not gonna live forever

*Blog link: [Ur not gonna live forever](https://timothydemoss.substack.com/p/breaking-ur-not-gonna-live-forever)*

I read this blog in the morning because this is what I have been feeling for a long time. There are so many things to do and I am not able to do all of them. I feel like I am missing out on building projects, reading books, and writing blogs.

This post hit me when I woke up and wanted to clear my saved articles in Substack. It highlights some of the ideas from the book **"Four Thousand Weeks"** by Oliver Burkeman.

The title comes from the average number of weeks in a human life. The book asks: How do you do all the things you want to do? And the honest answer is: You cannot.

Most productivity books tell you to wake up earlier, work harder, optimize your schedule. They assume that with enough effort, you can fit everything in. This book says that is wrong. You have finite time. No amount of optimization will change that.

The conclusion it arrives at is simple:

> **"Do few things that actually matter to you."**

I downloaded the book. I have to read it. Maybe I will find something useful for my situation.

---

## References

- Vidi. "How to be an AI researcher." YouTube, interview by Harnoor. [https://youtu.be/R-_Ra1z4Bn4](https://youtu.be/R-_Ra1z4Bn4)
- Dickson, B. "Escaping the chain-of-thought trap." TechTalks, Jun 2026. [https://bdtechtalks.substack.com/p/escaping-the-chain-of-thought-trap](https://bdtechtalks.substack.com/p/escaping-the-chain-of-thought-trap)
- Chopra, P. "How to approach research in AI." Lossfunk Letters, Jul 2025. [https://letters.lossfunk.com/p/how-to-approach-research-in-ai](https://letters.lossfunk.com/p/how-to-approach-research-in-ai)
- DeMoss, T. "Ur not gonna live forever." Tim DeMoss, Feb 2026. [https://timothydemoss.substack.com/p/breaking-ur-not-gonna-live-forever](https://timothydemoss.substack.com/p/breaking-ur-not-gonna-live-forever)
- Kambhampati, S. et al. "Position Paper: Chain-of-Thought Reasoning Without Chains." arXiv, 2025. [https://arxiv.org/abs/2504.09762](https://arxiv.org/abs/2504.09762)

---

*This post is a collection of things I learned today. Each section has a link to the original source so you can read more.*
