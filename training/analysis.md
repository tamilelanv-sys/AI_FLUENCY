# Agentic AI: Foundations and Open-Source Practice

## 1. Scenario

The scenario used in this project is a college fee assistance system. The system contains private course-fee information for three courses:

- CS101: ₹12,000
- AI202: ₹18,000
- DS303: ₹15,000

The same user queries are handled using three different approaches: a plain chatbot, a rule-based workflow, and an AI agent.

---

## 2. Plain Chatbot

The plain chatbot uses an LLM to understand the user's question and generate a response. It does not directly access the private course-fee data through external tools.

For a general question such as a welcome message, the chatbot can generate an appropriate response using its language-generation capability. However, when the user asks for an exact private fee, the chatbot cannot reliably retrieve the current value unless that information has already been provided to the model.

The main limitation is that the chatbot does not have a controlled mechanism for accessing the private fee database. Therefore, it may generate an answer without verifying the actual fee.

---

## 3. Rule-Based Workflow

The rule-based workflow uses predefined programming logic instead of an LLM to decide what actions should be performed.

For example, the program can check the requested course code, retrieve the corresponding fee from a predefined dictionary, perform calculations, and return the result.

This approach provides predictable and reproducible results because the program follows fixed rules. However, it has limited flexibility. Every possible type of request must be anticipated and represented in the programmed conditions.

For simple and clearly defined fee calculations, a rule-based workflow can provide reliable results. Its limitation becomes more visible when users ask questions that were not explicitly considered during implementation.

---

## 4. AI Agent

The AI agent combines an LLM, tools, and an execution loop.

The agent is provided with tools such as:

- `get_course_fee`
- `calculator`

The LLM receives the user's request and decides which tool should be used. The Python program executes the selected tool and returns the result to the LLM. The LLM can then decide whether another tool is required or whether it has enough information to produce the final response.

For example, for the question:

> What is the total fee for CS101 and AI202 after a 10% scholarship?

the agent can perform the following sequence:

1. Call `get_course_fee` for CS101.
2. Call `get_course_fee` for AI202.
3. Use `calculator` to calculate the total after the scholarship.
4. Generate the final response.

The expected calculation is:

`(12000 + 18000) × 0.90 = ₹27,000`

This demonstrates the Agent = LLM + Tools + Loop architecture.

The main advantage is that the agent can dynamically determine which tools are required for a multi-step request. However, its reliability depends on both the underlying model and the correctness of the tools. It can also require multiple LLM calls, which can increase latency.

---

## 5. Comparison

| Basis | Plain Chatbot | Rule-Based Workflow | AI Agent |
|---|---|---|---|
| Flexibility | High | Low | High |
| Decision-making | LLM-generated response | Predefined program logic | LLM selects next action |
| Tool usage | No external tools | Programmed functions | Dynamically selected tools |
| Private-data access | No direct controlled access | Yes | Yes, through tools |
| Multi-step task handling | Limited | Yes, if predefined | Yes, dynamically |
| Automation | Moderate | High | High |
| Reliability | Can vary | Predictable | Depends on model and tools |

---

## 6. Suitability Analysis

The three approaches are suitable for different types of problems.

A plain chatbot is suitable when the main requirement is natural-language interaction, explanation, or general question answering and no verified private data is required.

A rule-based workflow is suitable when the process is known in advance and predictable execution is more important than flexibility. For example, fixed fee lookups and predefined calculations can be implemented effectively using program logic.

An AI agent is suitable when a request requires multiple actions and the required tools may depend on the user's question. In the college-fee scenario, the agent can dynamically retrieve multiple course fees and then perform the required calculation.

Therefore, the agent demonstrates the greatest capability for dynamically handling the multi-step scenario, while the chatbot and workflow provide simpler alternatives for tasks that do not require dynamic tool selection.

---

## 7. Conclusion

This project demonstrates the difference between a plain chatbot, a rule-based workflow, and an AI agent.

A plain chatbot primarily uses an LLM to generate responses. A rule-based workflow follows predefined programming logic and provides predictable execution. An AI agent combines an LLM with tools and an execution loop, allowing it to select actions dynamically and continue working until the task is completed.

The comparison shows that the appropriate approach depends on the problem. Simple conversational tasks can use a chatbot, predictable processes can use rule-based workflows, and multi-step tasks involving tool selection can use an AI agent.
