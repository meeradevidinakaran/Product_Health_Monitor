# Product_Health_Monitor
A multi-agent multi modal AI workflow using ElevenLabs, that lets you query product health data by simply asking questions out loud.

# Multi Modal 
An agent becomes multi-modal when its perceive → reason → act loop spans more than one type of data.

# Problem Statement
TaskFlow, a project management SaaS product with 9,764 paying customers and $14.88M ARR, is experiencing growing pains. Support ticket volume has risen 25% month‑over‑month, Net Promoter Score (NPS) has dropped from 45 to 38, mobile app usage is down 15%, and the free‑to‑paid conversion rate has declined from 11.2% to 8.4%.The data needed to understand these problems exists across three separate sources:
⭐ User feedback (NPS surveys, app reviews, interview transcripts, in‑app submissions)
🎫 Support ticket analytics (Zendesk data showing volume, categories, trends, and churn risk)
📊 Product metrics (engagement data, conversion funnels, retention cohorts, performance benchmarks)

Answering critical questions such as “What are the top complaints this month?”, “Which enterprise accounts are at risk of churning?”, or “Is our conversion rate improving?” currently requires opening three different dashboards, exporting data, and cross‑referencing manually. **Each analysis takes 30–60 minutes, and this process is repeated multiple times a week.** 

# Goal
Build a multi‑agent voice AI system that enables product teams to query health and performance data simply by asking questions out loud. The system should leverage workflow orchestration to intelligently route each query to the appropriate specialist agent — whether the question is about user feedback, support tickets, or product metrics — ensuring accurate, context‑aware responses without manual dashboard cross‑referencing. Automating cross-functional data synthesis to enable data-driven decision-making for PM/ TPMs.

# Solution
We Will be using **Eleven Labs** platform to build our Multi modal agentic workflow. We will also evaluate the voice agents tone and optimize as per the requirement. 
We will have dedicated subagents for all three problem areas mentioned and distinct tone differences between subagents (e.g., the Feedback Analyst is empathetic, the Metrics Analyst is data-driven and crisp and Support Agent is helpful). We will use the **Gemini 2.5 Flash** LLM , select a preferred agent voices from Eleven labs library and also set up evaluation criteria.
<img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/d17f3840-7594-46ad-92d9-d9219e35b431" />

**Multiagent orchestration** - Here the Greeter node not only acts as a routing agent based on the intent but also confirms in case of ambiguity before the routing (below demo illustrates this feature) preventing hallucinations.

Each Subagent is equipped with relevant knowledge base and system prompts. Every Forward and Backward edge transitions among the agents are handled by LLM Conditions that act as **routing instructions**. Also the **interruptible** feature enables users to change topic mid-conversation; In such a scenario these cross routing edges have to re route to the correct subagent.


**Overview**
<img width="1920" height="1020" alt="Screenshot 2026-07-28 222224" src="https://github.com/user-attachments/assets/edb32c1f-d176-4178-89ee-fc5b80c9ce84" />

**Evaluation**
>> Evaluation criteria can be maintained under the **Analysis** tab for "Routing accuracy" , "Information retrieval success" or "Tone Adherence" etc. In our example below you can see the evaluation has been done for the "Tone adherence" and default LLM. The scoring and reasoning provided in the analysis tab post the conversation.

<img width="1920" height="1020" alt="Screenshot 2026-07-28 222238" src="https://github.com/user-attachments/assets/42785d6d-06c4-4169-b703-d9b984ad9d64" />

# Guardrails 

In Elevenlabs flash processes audio end to end there is no separate (Speech to Text) STT and (Text to speech)TTS step reducing latency or any emotion loss.
In each project there is a Global and Subagents framework that allow us to set quality gates at multiple levels.
ℹ️ Global Prompt allows to set instructions that is implicitly applicable to all the subagents in the workflow. ( ex- only use knowledge base data, avoid hallucinations, after answering politely ask if there's anything else required?" etc.)
ℹ️ Subagent Prompts help define a context and allow explicit redirections, format and conciseness and tone.
ℹ️ Elevenlabs also provide explicit guardrails feature where we can select the attributes we'd want to prevent in our agent's behaviour. Ex: Focus, manipulation , content or even create custom ones.
  
# Demo
https://github.com/user-attachments/assets/0910ce98-2127-4b2e-89b9-7e9ab5d41621

# Setup Instructions
![Setup_Instructions](docs/Setup_Instructions.md)

# System Design
![System Design](assets/VASystemDesign.png)

This System Design illustrates the Multi-Agent Orchestration layer. It highlights the use of a Greeter Agent for intent-based routing and Specialist Agents with scoped Knowledge Bases to ensure groundedness and eliminate cross-domain hallucinations

# Scaling Strategy
![Scaling_Strategy](docs/Scaling_Strategy.md)





