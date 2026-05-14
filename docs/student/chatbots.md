# Chatbots

When you are working on a question, you can open the workspace tab and chat with an AI assistant about the question you are on. This page explains what each chatbot is like and which one to pick.

![Chat Interface](images/chat_interface.png)

## What the chatbots can do

The chatbot already knows:

- The question you are on, all its parts, the final answer, and the worked solution
- Your teacher's guidance blurb and time estimate for the question
- The set the question is in (name, number, and description)
- Your full response history on each part: total submissions, wrong submissions, and your latest submission and the feedback you got
- How long you have spent on the question and current part today
- The full chat history you have had with the chatbot

So you don't need to copy-paste the question or re-explain what you've tried — just ask.

The chatbot is there to help you with **the specific question you are working on**. It won't help with unrelated material.

## Which chatbot should I use?

If your teacher chooses to turn on the chatbots for the module, you can choose from the following:

| Chatbot | Use this if you want… | How chatty | LLM | ~Response time |
|---|---|---|---|---|
| [Informational](#informational) | An explanation, or for it to walk you through the solution | Verbose | Gemini 2.5 Flash Lite (Google) | ~10s |
| [Concise](#concise) | A quick hint or clarification without a wall of text | Short | Gemini 2.5 Flash Lite (Google) | ~10s |
| [Reflective](#reflective) | To be nudged with questions instead of being given the answer | Asks you back | gpt-4o-mini (OpenAI) | ~10s |

For technical details behind each chatbot, see [Chat functions - More information](../advanced/chat_functions/info.md).

---
<!-- TODO: This information needs to be autoloaded in a similar manner to evaluation function documentation -->

## Informational Chatbot

A patient tutor that breaks problems into steps. It will give you hints first and only show the full answer only if you ask explicitly. It explains *why* you went wrong when you make a mistake, and tends to end its replies with a question to encourage further thinking or engagement.

**Example chat**

> **You:** How can I start solving this question?
>
> **Informational:** The question asks which of the given sets of equations represent possible three-dimensional incompressible flow cases. To determine this, we need to check the condition for incompressible flow for each case.
>
> Do you recall the mathematical condition for a flow to be incompressible?

**Tip:** if its explanation is longer than you need, ask "in one sentence, what should I do next?"

---

## Concise Chatbot

Short, direct answers and nothing else. No preamble, no examples, no details — unless you ask for them. Best when you just need one missing fact to get unstuck.

**Example chat**

> **You:** How can I start solving this question?
>
> **Concise:** Consider which governing equation applies to this problem.

**Tip:** if a hint is too short, ask it to explain *why* — it'll expand.

---

## Reflective Chatbot

A tutor that almost always replies with a question instead of an answer. It's trying to get you to work it out yourself by asking you to clarify, check your assumptions, or explain your reasoning.

**Example chat**

> **You:** How can I start solving this question?
>
> **Reflective:** What specific part of the question are you looking to tackle first, and what do you already understand about the concepts involved, such as the flow characteristics in a viscometer?

**Tip:** if you are truly stuck and the questions aren't helping, tell it what you have already tried and ask it to guide you through the problem.
