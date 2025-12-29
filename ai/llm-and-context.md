# TIL: State of LLMs and how to use them
**Date:** 2025-12-22
**Summary:** To make best use of AI and build useful applications, it'd be best to understand what LLMs really are (no, they are not magical black boxes) and why context matters.

## LLMs and Context Windows
An LLM is zip file containing the compressed, lossy, probabilistic model of the internet. In other words, it contains the "vibes" of the internet. Inside the zip file are the parameters of the neural network.

A context window is like a 1D token stream, which function like a working memory of an LLM for that particular conversation. In a chatbot setting, the user writes tokens to the context window for a bit, then the model, and back and forth. As can be seen when playing around with the context window length, if the AI context use exceeds the maximum window length, it will start to forget previously given information from the very same conversation. 

## Base LLMs and post-training
LLMs have 2 stages: pre-training and post-training. Pre-training costs significantly more, as it is attempting to compact the entire internet into one zip file. Post-training (supervised finetuning) is cheaper and attempts to train the model on thinking strategies.

ChatGPT will have perform better on knowledge-based conversations based on data that does not change over longer periods of time and are abundant on the internet.

Post-training with RL is a recent tactic introduced by Deepseek. When we see the "thought" processes of the thinking models, that is usually from the post-training stage. These models are particularly good at math and coding problems.

## Tooling
Base LLMs are zip files that are closed off and can respond only by text. Recent models have mechanisms to omit a special token that indicates that the application should stop sampling from the model and do an internet search with a given query. After getting the needed websites, it will place the data into the context window. This is the way to get the most up-to-date information from models.

Deep research is internet search + thinking. Deep research can still hallucination and hence must be treated as a "first draft" report.

Uploading files is basically adding those files to the context window.

ChatGPT has Python interpreters that can handle actual calculations, like multiplication. For smaller calculations, the model may have memorization to get the answer (and hence may hallucinate - this is probably the reason why it couldn't get the number of letters ins "strawberry" a while back). For larger calculations, it will convert the problem into a Python script to get the calcuation.

ChatGPT with audio options is saved as audio tokens, not text tokens. We can also re-represent images as tokens. This means the LLM can re-model images based on image tokens.

## Prompting
There are a couple of specifics that should be mentioned in prompts for better results.

- Personas  
Since LLMs are trained on the entirety of the internet, it's good to specify what domain of knowledge is needed in the prompt by specifying a persona.

- Context  
Provide relevant context to the model. LLMs are trained up to a point in time, so we need to provide more information to it.

- Fomat  
Specify what the output should look like to the LLM. Could directly reference an example of a good result.

- Chain of thought  
Tell the LLM to follow through with a chain of thoughts, by asking it to answer a series of clarifying questions before generating the output. This is the "extended thinking" or "reasoning models" in the big providers.

- Branching  
We can tell the LLM to come up with different options/branches of the output and compare to produce the best overall output.

But overall, the task/idea should be clear in my head if I want to be able to give the LLM clear prompts. In the end, all the prompts are tricks to articulate ourselves more clearly.

## Vibe coding wrong
Sean Grove (OpenAI) argues that the majority are vibe coding wrong. Most chat with an AI agent for hours, specifying the intentions and desired outputs, only to toss everything out and keeping the final code. Sean argues that it is equivalent to keeping JIT outputs while throwing away the source Java code. Instead, we should maintain our spec files and improve our ability to communicate with models.

The old approach: The majority use AI like a chatbot; no blame, since that's how it all started with ChatGPT. This approach revolves around back-and-forth conversations until the context runs out.

## Why does context matter?
People like to consider pieces of code as functions: you feed in input X, and you get output Y. LLMs are basically statless functions - the model does not change during inference and does not retain persistent knowledge of the codebase. The quality of the input (context) determines the quality of the output.

Thus, we don't want the agents to start from scratch each time to learn the entire codebase. Instead, we want to utilize "Frequent Internal Compaction" - we need to convey as much necessary contextual knowledge, problem space, and desired output as compact as possible.

## How to master context?
To "master" context, there are two strategies:
- provide persistent information via markdown files.
- use a proper workflow to compact knowledge and implement.
- do not outsource the thinking. AI is only able to amplify our own thinking (for now).

1. Research
> Understand the codebase/system, find all files relevant to the issue, comprehend how information flows, and stay objective (no extra bug hunting).

The purpose is to research and write down context relevant to the problem. This step will produce a research.md output file that the person should evaluate.

2. Planning
> Outline the exact implementation steps, include specific filenames/lines/snippets, and be super specific about the testing / verification steps in each phase.

The purpose is to plan out the changes to solve the problem. This step will produce a plan.md.

3. Implementing
> Step through the plan, phase by phase. For complex work, compact the current status back into the original plan file after each implementation phase is verified.



## AI tooling
### Subagents vs Commands
Commands are step-by-step orders to execute something immediately, usually initiated by a prefix. They operate within the shared context of your main conversation with the AI, meaning all the history and details are accessible. Commands are great for quick, one-off tasks where you want to stay in control, such as running a test on a file, listing available skills, or invoking a simple script.

Subagents AI agents that the main agent can delegate tasks to. It has its own independent context window, custom system prompt, tools, and expertise area.

One thing to note is that sub-agents are for managing context, not creating an identity for each bot.

## Expansion
Using this CLI + context management strategy is not limited to just coding. As Network Chuck shows, this can be used for a whole variety things, like YouTube scripting, document research, etc.

## Resources
- The New Code (OpenAI): https://www.youtube.com/watch?v=8rABwKRsec4
- Getting AI to work in complex codebases (Humanlayer): https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md
- Andrej Karpathy - How I use LLMs: https://www.youtube.com/watch?v=EWvNQjAaOHw
- Network Chuck's AI in CLI use: https://www.youtube.com/watch?v=MsQACpcuTkU
- Network Chuck's LLM context window explanation: https://www.youtube.com/watch?v=TeQDr4DkLYo
- Network Chuck's guide to prompting: https://www.youtube.com/watch?v=pwWBcsxEoLk