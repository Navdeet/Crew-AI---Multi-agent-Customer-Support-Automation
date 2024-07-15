Multi-AI-Agent-Systems-with-crewAI
This project is dedicated to automating business workflows using multi-agent AI systems. By leveraging the power of autonomous AI agents, this framework enables efficient and effective performance of complex, multi-step tasks.
Goal
Designing effective AI agents and organize team of AI agents them to perform complex, multi-step tasks.

AI Agents
When LLMs operate autonomously, they become agents. AI Agents ask and answer questions on its own.
LLMs + Cognition = AI Agents.

CrewAI
Framework for building multi-agent systems (that are autonomous, role-playing and collaborate)
Crew : Team of AI agents working together, each with a specific role.

Why Multi AI Agents rather single agent?
Assign specific role and specific task to each agent and improved output. Eg. One agent does exhaustive research and other does professional writing.
Use different LLMs for specific tasks


Applications of multi-agent systems.
Resume Strategist : Tailor resumes and interview prep
Design, build and test website
Research, write and fact-check technical papers
Automate customer support inquiries
Conduct social media campaigns
Perform financial analysis

What is Agentic Automation?
New way to write software. Provide fizzy inputs, apply fuzzy tranformations and get fuzzy outputs.


How Agentic Automation improves regular automation?
Regular Automation (Regular Data Collection and Analysis)
Capture information about the company
Use classification to generate scores for company
Prioritise for sales

Agentic Automation (Data Collection and Analysis using crew)
AI agent research about company (via Google, internal database)
AI agent compares companies (new ones, old ones)
AI agent scores companies (based on parameters)
AI agent provides intelligent questions to ask based on scores

Key Components of AI Agent
Role: Assign specialized role to agents
Memory: Provide agents with short-term, long-term and entity memory
Tools: Assign pre-built and custom tools to each agent (eg. for web search)
Focus: Break down task, goals and tools and assign multiple AI agents for better performance
Guardrails: Effectively handle errors, hallucinations and infinite loops.
Cooperation: Perform tasks in series, in parallel and hierarchical fashion
image image image

Role Playing
More specific role = Better response. Gives clear idea about agent's function in the crew.
Example: You are a financial analyst v/s you are FINRA approved financial analyst.

from crewai import Agent
agent = Agent(
  role='Data Analyst',
  goal='Extract actionable insights',
  backstory="""You're a data analyst at a large company.
  You're responsible for analyzing data and providing insights
  to the business.""")

Gaurdrails
Implemented at Framework level to prevrnt hallucinations, errors and infintite loops.

Memory
CrewAI provides short-term memory, long-term memory, entity memory, and newly identified contextual memory to help AI agents to remember, reason, and learn from past interactions.

Advantages of Memory
More contexual awareness, leading to more coherent and relevant responses
Experience Accumulation, learning from past actions to improve future decision-making and problem-solving.
Entity Understanding, agents can recognize and remember key entities, enhancing understanding.
image

Enable memory by setting memory=True in the Crew objects arguments.
from crewai import Crew, Agent, Task, Process

# Assemble your crew with memory capabilities
my_crew = Crew(
    agents=[...],
    tasks=[...],
    process=Process.sequential,
    memory=True,
    verbose=True
)
image

Mental Framework for Agent creations
Think of yourself as a Manager

Answer 3 questions:
What is the Goal ?
What is the Process ?
What kind of people I would like to hire, to get the work done
This will help to create agents (roles, goals, backstory)

What makes a great Tool ?
Versatile: Hndle Fuzzy inputs and provide strongly typed outputs
Caching Mechanism: Reuse previous results. Caching layer prevent unnecessary requests, stay within rate limits, speed up execution time
Error Handling: Gracefully handle erors & exceptions. How ? Sending error message to agent and ask agent to retry
NOTE: CrewAI supports both crewAI Toolkit and LangChain Tools

Mental Framework for Task creations
Think of yourself as a Manager

Ask what kind of process and tasks I expect individuals on my team to do.
Task requires min. 3 things:
description
expected_output
agent that will perform the task
image

Multi-agent Collaboration
Problem with Sequential Collaboration
Initial context fades away as tasks flows from agent to agent.

Advantages with Hierarchical Collaboration
Manager always remeber initial goal
Automatically delegates tasks
Asks agents for further improvement, if required.
