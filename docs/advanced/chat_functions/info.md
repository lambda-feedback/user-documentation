# Chat Functions - More information

Chat functions are the microservices that Lambda Feedback calls to provide the underlying functionality of a chatbot. Each chat function connects to a [Large Language Model (LLM)](https://uit.stanford.edu/service/techtraining/ai-demystified/llm) configured with its own role prompt, giving each chatbot its own personality and approach to assisting students.

For a higher-level description of the chatbots currently available and the context each one is given about the student and question, see the [Chatbots guide for teachers](../../teacher/guides/chatbots.md) (or the [student-facing version](../../student/chatbots.md)).

## Deployed chatbots
<!-- TODO: This information needs to be autoloaded in a similar manner to evaluation function documentation -->

The role prompts and key behaviours of the chatbots currently deployed on Lambda Feedback are described below.

### Informational Chatbot

**Role:** A patient AI tutor focused on student-centred learning — aims to foster critical thinking, active engagement, and confidence-building.

**Key behaviours from the role prompt**

- **Step-by-step guidance:** breaks problems into smaller steps and offers hints or intermediate steps before giving the final answer. Will share the complete answer if the student explicitly asks, but only after first encouraging exploration.
- **Error reflection:** treats mistakes as opportunities — helps the student work out *why* something went wrong rather than silently correcting it.
- **Awareness of materials:** grounds responses in the question's content, answer, worked solution, and the teacher's guidance — paraphrasing rather than quoting verbatim.
- **Adaptive support:** if the student keeps struggling, evaluates their progress and time spent on the question and gradually offers more detailed and specific guidance.
- **Engagement:** ends interactions with a question to keep the dialogue going and gauge comprehension.
- **Praise** is reserved for genuine effort or breakthroughs to avoid sounding insincere.
- **Stays on topic:** politely redirects students who ask about unrelated material.

[More details and source →](https://github.com/lambda-feedback/informationalChatFunction)

### Concise Chatbot

**Role:** A tutor that gives short, direct answers.

**Key behaviours from the role prompt**

- **Direct and minimal:** answers the question and stops — no extra details, explanations, or examples unless the student asks.
- **Aware of struggle:** if the student seems stuck or frustrated, references their progress so far and how long they have spent on the question relative to the teacher's guidance time.
- **Stays on topic:** redirects unrelated questions back to the current material with a short refusal.
- **No filler:** does not end messages with concluding statements or summaries.

[More details and source →](https://github.com/lambda-feedback/conciseChatFunction)

### Reflective Chatbot

**Role:** A Socratic tutor that guides students to discover knowledge through questioning rather than direct instruction.

**Key behaviours from the role prompt**

- **Always ends with a question:** every response finishes with a follow-up question that pushes the student's thinking forward.
- **Counter-questions over answers:** when a student asks a direct question, responds with a question that guides them toward the answer rather than handing it over. If it does share a fact, it immediately follows with a question that asks the student to apply or extend it.
- **Uses a varied question toolkit:** clarifying ("What do you mean by…?"), assumption-probing ("What are you assuming here?"), evidence-based, perspective, implication, and meta-questions about why a question matters.
- **Diagnoses where the student is stuck:** if a student is frustrated, asks about their thought process to locate the gap, drawing on their progress and time spent.
- **Never provides complete answers:** always leaves room for the student to think and respond.

[More details and source →](https://github.com/lambda-feedback/reflectiveChatFunction)

## Chat Function Development

Are you interested in developing your own chatbot? Check out the [Quickstart guide](quickstart.md) to develop and deploy your own AI chat function for Lambda Feedback.
