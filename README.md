Multi-AI-Agent-Systems-with-crewAI
This project is dedicated to automating business workflows using multi-agent AI systems. By leveraging the power of autonomous AI agents, this framework enables efficient and effective performance of complex, multi-step tasks.

Goal
Designing effective AI agents and organize team of AI agents them to perform complex, multi-step tasks.

Why AI Agents better than LLMs
LLMs
Provide human feedback iteratively to fine-tune response

AI Agents
When LLMs operate autonomously, they become agents. AI Agents ask and answer questions on its own.

LLMs + Cognition = AI Agents.

image

Source: deeplearning.ai

crewAI
Framework for building multi-agent systems (that are autonomous, role-playing and collaborate)
crew : Team of AI agents working together, each with a specific role.

Why Multi AI Agents rather single agent
Assign specific role and specific task to each agent and improved output. Eg. One agent does exhaustive research and other does professional writing.
Use different LLMs for specific tasks
image image

Source: deeplearning.ai

Applications of multi-agent systems.
Resume Strategist : Tailor resumes and interview prep
Design, build and test website
Research, write and fact-check technical papers
Automate customer support inquiries
Conduct social media campaigns
Perform financial analysis
What is Agentic Automation
New way to write software. Provide fizzy inputs, apply fuzzy tranformations and get fuzzy outputs.

Reason why people love chatGPT: Probablistic nature

image

Source: deeplearning.ai

How Agentic Automation improves regular automation
Regular Automation (Regular Data Collection and Analysis)
Capture information about the company
Use classification to generate scores for company
Prioritise for sales
image

Source: deeplearning.ai

Agentic Automation (Data Collection and Analysis using crew)
AI agent research about company (via Google, internal database)
AI agent compares companies (new ones, old ones)
AI agent scores companies (based on parameters)
AI agent provides intelligent questions to ask based on scores
image

Source: deeplearning.ai

Key Components of AI Agent
Role: Assign specialized role to agents
Memory: Provide agents with short-term, long-term and entity memory
Tools: Assign pre-built and custom tools to each agent (eg. for web search)
Focus: Break down task, goals and tools and assign multiple AI agents for better performance
Guardrails: Effectively handle errors, hallucinations and infinite loops.
Cooperation: Perform tasks in series, in parallel and hierarchical fashion
image image image

Source: deeplearning.ai

Role Playing
More specific role = Better response. Gives clear idea about agent's function in the crew.

Example: You are a financial analyst v/s you are FINRA approved financial analyst.

from crewai import Agent

agent = Agent(
  role='Data Analyst',
  goal='Extract actionable insights',
  backstory="""You're a data analyst at a large company.
  You're responsible for analyzing data and providing insights
  to the business."""
)
Focus
Assinging too many tasks, tools, context to a single agent, cause losing essential information and hallucinate.

Therefore, break down task, goals and tools and assign to multiple AI agents for better performance

research_ai_task = Task(
    description='Find and summarize the latest AI news',
    expected_output='A bullet list summary of the top 5 most important AI news',
    agent=research_agent,
    tools=[search_tool]
)

research_ops_task = Task(
    description='Find and summarize the latest AI Ops news',
    expected_output='A bullet list summary of the top 5 most important AI Ops news',
    agent=research_agent,
    tools=[search_tool]
)

write_blog_task = Task(
    description="Write a full blog post about the importance of AI and its latest news",
    expected_output='Full blog post that is 4 paragraphs long',
    agent=writer_agent,
    context=[research_ai_task, research_ops_task]
)
Tools
Assign tools to AI Agents and Tasks for improving execution and performance.

from crewai import Agent

researcher = Agent(
    role='Market Research Analyst',
    goal='Provide up-to-date market analysis of the AI industry',
    backstory='An expert analyst with a keen eye for market trends.',
    tools=[search_tool, web_rag_tool]
)
Note: Tasks specific tools override an agent's default tools.

task = Task(
  description='Find and summarize the latest AI news',
  expected_output='A bullet list summary of the top 5 most important AI news',
  agent=research_agent,
  tools=[search_tool]
)
Collaboration
Agents collobrate to combine skills, share information, delegate tasks to each other.

Sequential Collaboration
Ideal for projects requiring tasks to be completed in a specific order.

report_crew = Crew(
  agents=[researcher, analyst, writer],
  tasks=[research_task, analysis_task, writing_task], # tasks executed in the order of listing, with output of one task serving as context for the next
  process=Process.sequential
)
Hierarchical Collaboration
CrewAI automatically creates a manager agent, requiring the specification of a manager language model (manager_llm) for the manager agent.
THe manager allocates tasks among crew members based on their roles, tools and capabilities.
The manager evaluates outcomes to ensure they meet the required standards.
set Process attribute to Process.hierarchical for Crew object
set manager_llm for Crew Object. Mandatory for hierarchical process
from crewai import Crew
from crewai.process import Process
from langchain_openai import ChatOpenAI

# Example: Creating a crew with a hierarchical process
# Ensure to provide a manager_llm
crew = Crew(
    agents=my_agents,
    tasks=my_tasks,
    process=Process.hierarchical,
    manager_llm=ChatOpenAI(model="gpt-4")
)
Parallel Collaboration
Tasks can now be executed asynchronously, allowing for parallel processing and efficiency improvements

list_ideas = Task(
    description="List of 5 interesting ideas to explore for an article about AI.",
    expected_output="Bullet point list of 5 ideas for an article.",
    agent=researcher,
    async_execution=True # Will be executed asynchronously
)

list_important_history = Task(
    description="Research the history of AI and give me the 5 most important events.",
    expected_output="Bullet point list of 5 important events.",
    agent=researcher,
    async_execution=True # Will be executed asynchronously
)

write_article = Task(
    description="Write an article about AI, its history, and interesting ideas.",
    expected_output="A 4 paragraph article about AI.",
    agent=writer,
    context=[list_ideas, list_important_history] # Will wait for the output of the two tasks to be completed
)
Gaurdrails
Implemented at Framework level to prevrnt hallucinations, errors and infintite loops.

Memory
CrewAI provides short-term memory, long-term memory, entity memory, and newly identified contextual memory to help AI agents to remember, reason, and learn from past interactions.

Advantages of Memory

More contexual awareness, leading to more coherent and relevant responses
Experience Accumulation, learning from past actions to improve future decision-making and problem-solving.
Entity Understanding, agents can recognize and remember key entities, enhancing understanding.
image

Source: deeplearning.ai

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

Source: deeplearning.ai

Mental Framework for Agent creations
Think of yourself as a Manager

Answer 3 questions:

What is the Goal ?
What is the Process ?
What kind of people I would like to hire, to get the work done
This will help to create agents (roles, goals, backstory)

image

Source: deeplearning.ai

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

Source: deeplearning.ai

Multi-agent Collaboration
Problem with Sequential Collaboration
Initial context fades away as tasks flows from agent to agent.

image

Source: deeplearning.ai

Advantages with Hierarchical Collaboration
Manager always remeber initial goal
Automatically delegates tasks
Asks agents for further improvement, if required.
