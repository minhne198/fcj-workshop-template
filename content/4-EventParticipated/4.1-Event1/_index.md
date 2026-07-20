---
title: "Event 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

## Reflection Report: "Automated Prompt Engineering: Enhancing LLM Output Quality"

### Event Purpose

* Share effective communication techniques with Artificial Intelligence (AI).
* Explain the importance of Prompt Engineering in cost and performance optimization.
* Introduce the core components of a high-quality prompt.
* Present advanced prompting techniques and workflow automation tools.

### Speakers

* **Nguyen Tuan Thinh** - DevOps/Cloud Engineer at First Cloud AI Journey.

### Highlighted Content

#### The importance of Prompt Engineering

Using prompts that are too generic can lead to several issues:

* **Token waste:** Increases AI usage cost unnecessarily.
* **Inconsistent output:** Vague instructions cause low-quality responses.
* **Reduced productivity:** Users spend time adjusting prompts repeatedly instead of getting useful results quickly.

#### Key components of a great prompt

For AI to work accurately, a prompt should include 7 elements:

1. **Role:** Set the model's role, such as "You are a career consultant."
2. **Instruction:** Clearly state the task to perform.
3. **Context:** Provide relevant background information.
4. **Input Data:** Include the specific data that must be processed.
5. **Output Format:** Define the output structure, such as JSON or Markdown.
6. **Examples:** Provide sample outputs or few-shot examples.
7. **Constraints:** Specify limits such as length, language, or rules to follow.

#### Token Economics

* Understand how AI pricing is calculated based on tokens, which are smaller units than words.
* Distinguish between input token cost and output token cost to optimize budget.

#### Advanced prompting techniques

* **Chain-of-Thought (CoT):** Guide AI to reason step by step for more logical results.
* **Self-Consistency:** Run multiple reasoning paths and select the most common result.
* **Tree-of-Thoughts (ToT):** Allow AI to explore multiple problem-solving directions.
* **RAG (Retrieval-Augmented Generation):** Combine external data sources so AI can answer more accurately.

#### Proptimizer tool

* Introduced a browser extension that helps optimize prompts on the web.
* The system architecture is based on AWS services such as **Amazon Bedrock**, **AWS Lambda**, and **Amazon DynamoDB**.

### Lessons Learned

#### Technical mindset

* **Be Clear & Specific:** Always prioritize specific wording and direct instructions.
* **Describe DOs, not DON'Ts:** Focus on what the AI should do instead of only listing restrictions.
* **Separate data clearly:** Use delimiters to separate instructions, context, and input data.

#### Optimization strategy

* Break complex requirements into smaller parts so AI can process them more effectively.
* Accept "I don't know" answers from AI when needed to reduce hallucination.

### Application to Study and Work

* Optimize prompts for writing test cases and analyzing business requirements.
* Use CoT techniques to ask AI to solve complex programming logic in Java and Flutter.
* Experiment with Proptimizer to work faster with documents in the browser.

### Event Experience

* I gained deeper knowledge about how large language models operate.
* I understood the AWS infrastructure behind modern AI applications through Solution Architecture diagrams.
* The workshop provided many practical examples, from writing social media posts to improving self-introduction content for fresh graduates.

#### Some photos from the event

![Event photo 1](/images/ev1.jpg)
![Event photo 2](/images/ev11.jpg)

Overall, the event not only provided technical knowledge but also helped me change the way I think about application design, system modernization, and effective collaboration between teams.
