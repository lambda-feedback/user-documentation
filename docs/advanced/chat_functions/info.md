# Chat Functions - More information

Chat functions are the microservices that Lambda Feedback calls to provide the underlying functionality of a chatbot. Students can chat with the chatbots and ask for help or further explanations regarding the Question that they are working on. Each chatbot has its own personality and approach to assisting the students.

The chatbots have at their basis a [Large Language Model (LLM)](https://en.wikipedia.org/wiki/Large_language_model) which received information regarding:

- The raw markdown content of the question the student is on currently, including:
    - The question name, number and content
    - The final answer, structured tutorial, and worked solutions of the question
    - The guidance (blurb and time estimate) from the teacher for the question
    - The set name, number and description
    - All parts with their number, content and done status (current part emphasised)
    - All response areas and their respective expected answers
- The progress of the student on all parts of the Question, including:
    - The total number of responses and the number of wrong responses the student has made for each response area
    - The last responses the student has made for each response area and the received feedback
    - The time duration the student has spent on the respective question and current part on that day

---

## Available Chat functions

Currently the students have access to the following chat functions that host their own specific chatbot. Many others are in development.

Click on the links below for information on each chatbot:

[1. Informational Chatbot](https://github.com/lambda-feedback/informationalChatFunction/blob/main/docs/user.md)


[2. Concise Chatbot](https://github.com/lambda-feedback/conciseChatFunction/blob/main/docs/user.md)


[3. Reflective Chatbot](https://github.com/lambda-feedback/reflectiveChatFunction/blob/main/docs/user.md)


## Chat Function Development

Are you interested in developing your own chatbot? Then check out the [Quickstart guide](quickstart.md) to develop and deploy your own AI chat function for Lambda Feedback.
