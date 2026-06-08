# Project Proposal: Parameterizing Agentic AI Architectures Beyond Task Performance

## 1. Working Title

**Toward a Formal Parameterization Framework for Agentic AI Architectures**

Alternative titles:

* **An Architecture Vector for Comparing Agentic AI Systems**
* **Beyond Benchmarks: Structural Metrics for Agentic AI Systems**
* **Quantifying Design Patterns in LLM-Based Agent Architectures**

---

## 2. Problem Statement

Agentic AI systems are increasingly built using recurring design patterns such as ReAct loops, planner-executor systems, reflection loops, tool-using agents, memory-augmented agents, and multi-agent supervisor-worker architectures. Current evaluation practices usually focus on task success, benchmark performance, latency, cost, or correctness.

However, these metrics do not fully describe the **architecture** of an agentic system.

Two systems may achieve similar task success while having very different internal structures. For example, one system may be a single ReAct-style agent with dynamic tool use, while another may use a planner, multiple specialist agents, long-term memory, reflection, human approval gates, and structured tool permissions. Existing benchmarks can compare their outputs, but they do not provide a formal vocabulary for comparing their architectural complexity, autonomy, coordination structure, memory design, tool coupling, or control topology.

This project proposes a formal framework for **parameterizing agentic AI architectures** independently of downstream task performance.

---

## 3. Motivation

As agentic systems move from simple chat interfaces to production systems that plan, use tools, interact with APIs, coordinate multiple agents, and take actions in external environments, architecture-level analysis becomes increasingly important.

Without a formal parameterization framework, researchers and engineers struggle to answer questions such as:

* How structurally different are two agentic systems?
* Is a multi-agent design actually more complex than a single-agent design?
* How much autonomy does a system have?
* How deeply is memory integrated into the decision loop?
* How centralized or decentralized is coordination?
* How many authority boundaries exist between reasoning and action?
* Can we describe agentic architectures in a reusable, model-independent way?

This gap matters because architecture affects reliability, safety, observability, maintainability, governance, and cost even when task-level performance appears similar.

---

## 4. Research Objective

The objective of this project is to design and validate a formal **Agent Architecture Parameterization Framework** that can describe and compare agentic AI systems at the structural level.

The project will define a set of architectural dimensions, assign each dimension measurable or ordinal values, and apply the framework to representative agentic systems such as:

* ReAct
* Toolformer-style tool-using agents
* Reflexion
* Tree of Thoughts
* Graph of Thoughts
* Generative Agents
* Voyager
* AutoGen
* MetaGPT
* SWE-agent
* Enterprise-style human-in-the-loop agents

The final output will be a taxonomy, scoring rubric, and architecture vector that allows two agentic systems to be compared without relying only on task success.

---

## 5. Core Research Question

**How can agentic AI systems be formally parameterized based on architectural characteristics rather than task performance?**

---

## 6. Sub-Questions

1. What are the recurring architectural dimensions across modern LLM-based agent systems?
2. Which dimensions can be represented as categorical, ordinal, graph-based, or numerical parameters?
3. Can existing agentic design patterns be mapped into a common architecture vector?
4. How can architectural complexity be measured in agentic systems?
5. What trade-offs become visible when comparing systems through architectural parameters instead of benchmark scores?
6. Can this framework help explain differences in safety, observability, control, and maintainability?

---

## 7. Literature Survey

### 7.1 Foundations of LLM-Based Agents

Early LLM-agent work introduced the idea of language models as systems that do more than generate text. Instead of responding once to a prompt, agents can reason, act, observe feedback, call tools, update state, and continue operating across multiple steps.

The ReAct framework is one of the foundational works in this area. It combines reasoning traces with actions in an interleaved loop. The key architectural contribution is not only improved task performance, but the introduction of a reusable control structure: reason, act, observe, and repeat.

Toolformer introduces another important architectural idea: language models can learn when and how to call external tools. This makes tool use a first-class component of the agent architecture. From a parameterization perspective, Toolformer is relevant because it raises questions about tool selection, tool invocation policies, and how tightly tools are integrated into the model’s reasoning process.

The survey “A Survey on Large Language Model based Autonomous Agents” provides a broad organization of the field around agent construction, application, and evaluation. It is useful as a high-level map of the agent landscape, but it still primarily surveys capabilities and applications rather than defining precise architecture metrics.

### 7.2 Reasoning and Planning Architectures

A major line of work focuses on how agents plan and reason over multiple steps.

Tree of Thoughts extends chain-of-thought reasoning by allowing the model to explore multiple reasoning branches, evaluate intermediate thoughts, and backtrack when necessary. Architecturally, this introduces a search-based control flow rather than a simple linear reasoning path.

Graph of Thoughts generalizes this further by representing intermediate thoughts as nodes in a graph, with dependencies or transformations represented as edges. This is especially relevant for architecture parameterization because it suggests that reasoning structures can be compared using graph properties such as branching factor, depth, cyclicity, and dependency structure.

Reflexion introduces verbal reinforcement through self-reflection. Instead of updating model weights, the agent stores feedback in memory and uses it to improve future attempts. This makes reflection and episodic memory explicit architectural components.

These works show that reasoning architecture can be parameterized by planning depth, branching factor, search topology, feedback loops, and self-evaluation mechanisms.

### 7.3 Memory-Augmented Agent Architectures

Memory is one of the most important architectural dimensions of agentic systems.

Generative Agents introduced an architecture where agents store observations, retrieve memories, synthesize reflections, and plan future behavior. This work is important because memory is not treated as a passive chat history. Instead, memory is structured, retrieved, summarized, and used to drive behavior.

Voyager extends this idea in an embodied environment. It uses an automatic curriculum, an executable skill library, and iterative prompting with environmental feedback. From an architectural perspective, Voyager is important because it separates memory into reusable skills rather than only storing natural language traces.

CoALA, or Cognitive Architectures for Language Agents, is one of the most directly relevant papers for this project. It proposes a modular view of language agents using memory components, structured action spaces, and decision-making procedures. CoALA connects LLM agents to older work in cognitive architectures and provides a strong conceptual foundation for architecture-level comparison.

Memory can therefore be parameterized by:

* memory type
* memory persistence
* retrieval mechanism
* memory update policy
* memory visibility
* memory granularity
* whether memory stores text, embeddings, symbolic state, executable skills, or structured records

### 7.4 Multi-Agent Architectures

Multi-agent systems introduce additional architectural dimensions beyond single-agent systems.

AutoGen presents a framework for building LLM applications using multiple conversable agents. Agents can use LLMs, human input, and tools, while developers define interaction patterns among them. This makes communication topology and agent role design central architectural parameters.

MetaGPT proposes a multi-agent software engineering architecture based on standardized operating procedures and role specialization. It uses an assembly-line style workflow where agents represent roles such as product manager, architect, engineer, and reviewer. This is important because it shows that multi-agent systems can be parameterized by role decomposition, workflow constraints, and coordination protocol.

Surveys on LLM-based multi-agent systems organize the field around components such as profile, perception, self-action, mutual interaction, and evolution. Other survey work focuses specifically on collaboration mechanisms, including cooperation, competition, centralized structures, peer-to-peer structures, role-based strategies, and coordination protocols.

These works suggest that multi-agent architectures can be parameterized using:

* number of agents
* role specialization
* communication graph
* coordination topology
* authority distribution
* shared vs private memory
* centralized vs decentralized control
* collaboration protocol
* conflict resolution mechanism

### 7.5 Agent-Computer Interfaces and Environment Coupling

SWE-agent argues that agents need specially designed interfaces to interact effectively with software environments. This introduces the idea of an Agent-Computer Interface, or ACI.

This is important for architecture parameterization because the environment interface is not neutral. The tools, commands, feedback channels, file-editing interface, and test execution loop all shape how the agent behaves.

A system with a rich structured interface is architecturally different from a system that interacts with the environment only through natural language. Therefore, environment coupling should be treated as a formal parameter.

Relevant parameters include:

* action space size
* action structure
* feedback richness
* tool affordances
* reversibility of actions
* permission boundaries
* observability of environment state

### 7.6 Taxonomies and Evaluation Surveys

Recent survey work has started to define taxonomies for LLM agents, multi-agent systems, and agent evaluation. These surveys are useful but do not yet fully solve the problem addressed in this project.

Existing surveys commonly classify agents by:

* reasoning
* planning
* memory
* tool use
* perception
* action
* multi-agent collaboration
* evaluation
* application domain

However, most of these taxonomies remain qualitative. They identify components but do not convert them into measurable architecture parameters.

The gap is that there is no widely accepted equivalent of a “complexity vector” or “architecture signature” for agentic systems.

---

## 8. Identified Research Gap

The literature provides:

* design patterns
* agent frameworks
* qualitative taxonomies
* task benchmarks
* evaluation methods
* multi-agent collaboration surveys

But it does not yet provide a rigorous and reusable way to describe agentic systems as parameterized architectures.

Specifically, existing work lacks:

1. A compact architecture vector for representing agentic systems.
2. Metrics for agentic control-flow complexity.
3. Metrics for memory integration complexity.
4. Metrics for tool-coupling and authority boundaries.
5. Metrics for multi-agent communication topology.
6. A way to compare systems structurally even when they solve different tasks.
7. A design-review framework for choosing between agentic patterns.

This project addresses that gap.

---

## 9. Proposed Framework: Agent Architecture Vector

This project proposes representing an agentic system as an architecture vector:

```text
A = <G, C, P, M, T, R, H, O, F, S>
```

Where:

| Symbol | Dimension                   | Meaning                                                         |
| ------ | --------------------------- | --------------------------------------------------------------- |
| G      | Goal structure              | How goals are represented, decomposed, and updated              |
| C      | Control topology            | Linear, cyclic, tree, graph, planner-executor, hierarchical     |
| P      | Planning depth              | How far the system plans ahead and whether it replans           |
| M      | Memory model                | Type, persistence, retrieval, update policy, and visibility     |
| T      | Tool/action model           | Tool count, structure, permissions, and invocation policy       |
| R      | Reflection/evaluation loop  | Presence of critique, verification, debate, or self-improvement |
| H      | Human oversight             | Approval gates, escalation rules, and collaboration mode        |
| O      | Observability               | Traceability, replayability, state inspection, and audit logs   |
| F      | Failure recovery            | Retry, fallback, replanning, rollback, or human escalation      |
| S      | Safety/authority boundaries | Read/write permissions, side-effect risk, policy enforcement    |

---

## 10. Candidate Metrics

### 10.1 Agency Level

Measures what the system is capable of doing.

Possible scale:

| Level | Description                                            |
| ----- | ------------------------------------------------------ |
| 0     | Text-only response                                     |
| 1     | Can suggest actions                                    |
| 2     | Can call read-only tools                               |
| 3     | Can call write-capable tools with approval             |
| 4     | Can execute reversible actions autonomously            |
| 5     | Can execute irreversible external actions autonomously |

### 10.2 Autonomy Level

Measures how independently the system acts.

| Level | Description                                               |
| ----- | --------------------------------------------------------- |
| 0     | Fully human-directed                                      |
| 1     | Human selects each step                                   |
| 2     | Agent proposes, human approves                            |
| 3     | Agent acts within a fixed workflow                        |
| 4     | Agent dynamically plans and acts                          |
| 5     | Agent sets subgoals, replans, and acts over long horizons |

### 10.3 Control-Flow Complexity

Possible features:

* number of decision nodes
* number of loops
* maximum planning depth
* branching factor
* presence of backtracking
* graph cyclicity
* number of termination conditions

Example:

```text
Control Complexity = loops + branches + replanning points + feedback edges
```

### 10.4 Agent Coordination Complexity

For multi-agent systems:

* number of agents
* number of communication edges
* graph density
* centralization score
* number of role types
* shared memory access count
* conflict resolution mechanism

Example:

```text
Coordination Density = actual communication edges / possible communication edges
```

### 10.5 Memory Complexity

Possible features:

* memory layers
* persistence duration
* retrieval methods
* write policies
* summarization mechanisms
* memory sharing scope
* structured vs unstructured memory

Example scale:

| Level | Description                                                        |
| ----- | ------------------------------------------------------------------ |
| 0     | No memory                                                          |
| 1     | Conversation buffer                                                |
| 2     | Retrieved context                                                  |
| 3     | Long-term vector memory                                            |
| 4     | Structured symbolic memory                                         |
| 5     | Multi-layer memory with reflection, consolidation, and skill reuse |

### 10.6 Tool Coupling

Possible features:

* number of tools
* read vs write tools
* tool schema complexity
* dynamic vs fixed tool selection
* tool permission model
* reversibility of tool effects

### 10.7 Reflection and Self-Correction

Possible scale:

| Level | Description                                      |
| ----- | ------------------------------------------------ |
| 0     | No reflection                                    |
| 1     | Simple final self-check                          |
| 2     | Step-level critique                              |
| 3     | Separate verifier or critic                      |
| 4     | Persistent reflective memory                     |
| 5     | Multi-agent debate or iterative self-improvement |

### 10.8 Observability

Possible features:

* trace logs
* tool call logs
* state snapshots
* replay support
* memory inspection
* cost per step
* decision provenance

### 10.9 Authority Boundary Score

Measures how much real-world authority the agent has.

Possible parameters:

* read-only vs write access
* access to external APIs
* ability to affect users, money, infrastructure, files, or production systems
* approval gates
* rollback support

---

## 11. Methodology

### Phase 1: Literature Review

Survey representative papers across:

* single-agent reasoning systems
* tool-using agents
* reflection-based agents
* memory-augmented agents
* embodied agents
* multi-agent systems
* agent-computer interfaces
* agent taxonomies
* evaluation surveys
* software architecture and governance papers

The goal is to extract recurring architectural features.

### Phase 2: Dimension Extraction

Create a coding sheet for each paper/system.

For each system, record:

* number of agents
* role structure
* control flow
* memory type
* tool model
* planning strategy
* reflection mechanism
* human involvement
* failure handling
* observability
* authority boundaries

### Phase 3: Architecture Vector Design

Convert the qualitative coding sheet into an architecture vector with categorical, ordinal, and graph-based dimensions.

Example:

```text
ReAct = <goal: implicit, control: cyclic, planning: shallow, memory: local context, tools: dynamic read tools, reflection: none, human: none, observability: traceable, failure: observe-retry, safety: low-write>
```

### Phase 4: Case Study Mapping

Apply the framework to selected systems:

| System            | Main Architectural Pattern                        |
| ----------------- | ------------------------------------------------- |
| ReAct             | single-agent reason-act loop                      |
| Toolformer        | learned tool-use policy                           |
| Reflexion         | reflective memory loop                            |
| Tree of Thoughts  | search-based reasoning                            |
| Graph of Thoughts | graph-structured reasoning                        |
| Generative Agents | memory-reflection-planning architecture           |
| Voyager           | embodied lifelong learning with skill library     |
| AutoGen           | multi-agent conversation framework                |
| MetaGPT           | SOP-based role-specialized multi-agent workflow   |
| SWE-agent         | agent-computer interface for software engineering |

### Phase 5: Comparative Analysis

Compare systems using:

* architecture vectors
* radar charts
* communication graphs
* control-flow diagrams
* complexity scores
* qualitative trade-off discussion

### Phase 6: Validation

Validate the framework using expert review or consistency checks.

Possible validation methods:

1. Apply the framework to known systems and check whether it distinguishes them meaningfully.
2. Ask multiple reviewers to independently parameterize the same systems and measure agreement.
3. Compare architectural complexity scores with qualitative expectations from the literature.
4. Use case studies to show how the framework supports design decisions.

---

## 12. Expected Contributions

This project will produce:

1. A literature survey of agentic AI architecture patterns.
2. A formal set of architecture dimensions for parameterizing agentic systems.
3. An Agent Architecture Vector for comparing systems.
4. A scoring rubric for autonomy, agency, memory, planning, coordination, and authority.
5. A comparative analysis of representative agentic systems.
6. A discussion of open research questions in architecture-level agent evaluation.

---

## 13. Example Comparative Table

| System            | Agents | Control Flow              | Memory              | Tool Use            | Reflection         | Human Role        | Architecture Notes             |
| ----------------- | -----: | ------------------------- | ------------------- | ------------------- | ------------------ | ----------------- | ------------------------------ |
| ReAct             |      1 | cyclic reason-act-observe | context only        | dynamic tools       | no                 | none              | foundational action loop       |
| Toolformer        |      1 | model-driven tool call    | implicit            | learned API calls   | no                 | none              | tool invocation policy         |
| Reflexion         |      1 | trial-reflect-retry       | episodic reflection | optional            | yes                | none              | verbal RL via memory           |
| Tree of Thoughts  |      1 | tree search               | local search state  | no/optional         | self-eval          | none              | branching reasoning            |
| Graph of Thoughts |      1 | graph reasoning           | graph state         | no/optional         | feedback loops     | none              | arbitrary thought graph        |
| Generative Agents |   many | observe-reflect-plan-act  | long-term memory    | environment actions | yes                | user can interact | social simulation architecture |
| Voyager           |      1 | curriculum-execute-refine | skill library       | code execution      | self-verification  | none              | lifelong embodied learning     |
| AutoGen           |   many | conversational topology   | configurable        | configurable        | configurable       | optional          | general multi-agent framework  |
| MetaGPT           |   many | SOP workflow              | shared artifacts    | role-specific       | review stages      | none              | assembly-line collaboration    |
| SWE-agent         |      1 | iterative software loop   | repo state          | shell/editor/tests  | implicit via tests | none              | ACI-centered architecture      |

---

## 14. Potential Deliverables

* Final report
* Architecture taxonomy
* Architecture vector specification
* Case study matrix
* Diagram of agentic architecture design space
* Python notebook or spreadsheet for scoring systems
* Short design guide: “How to choose an agent architecture”
* Optional prototype: small tool that takes an agent architecture description and outputs its architecture vector

---

## 15. Evaluation Plan

Because this project is not mainly about task performance, evaluation will focus on the usefulness and consistency of the parameterization framework.

### Evaluation Criteria

| Criterion            | Question                                                        |
| -------------------- | --------------------------------------------------------------- |
| Coverage             | Can the framework describe many agentic systems?                |
| Discriminative power | Does it distinguish systems that are architecturally different? |
| Interpretability     | Can engineers understand the dimensions?                        |
| Reproducibility      | Do different reviewers assign similar values?                   |
| Design usefulness    | Does it help choose between architectures?                      |
| Extensibility        | Can new agent patterns be added?                                |

### Possible Validation Study

Select 10 agentic systems and have 2-3 reviewers independently fill out the architecture vector. Then calculate agreement for each dimension.

Dimensions with low agreement may need clearer definitions.

---

## 16. Risks and Limitations

1. Some architecture details are not fully disclosed in papers.
2. Many systems are described at a high level, making precise parameterization difficult.
3. Some dimensions may be subjective.
4. The framework may overfit to current LLM-agent patterns.
5. The line between architecture and implementation can be blurry.
6. Scoring systems may imply false precision if not carefully defined.

---

## 17. Open Research Questions

1. Can agentic architecture complexity be measured similarly to software complexity?
2. Is multi-agent architecture always more complex than single-agent architecture?
3. Can communication topology predict failure modes?
4. How should memory complexity be measured?
5. How should tool authority be represented formally?
6. Can architecture vectors predict maintainability or safety risk?
7. Can architecture parameters guide automated agent design?
8. Can agent systems be compiled from architecture specifications?

---

## 18. Proposed Timeline

### Week 1: Literature Collection

* Collect 20-30 papers.
* Categorize by agent pattern.
* Build annotated bibliography.

### Week 2: Taxonomy Extraction

* Extract recurring architectural features.
* Group them into dimensions.
* Draft initial architecture vector.

### Week 3: Metric Design

* Define ordinal scales.
* Define graph-based metrics for communication and control flow.
* Define memory and tool-coupling metrics.

### Week 4: Case Study Mapping

* Apply framework to 8-10 known systems.
* Create comparison tables.
* Identify ambiguous dimensions.

### Week 5: Validation

* Perform reviewer consistency check or self-consistency analysis.
* Refine scoring definitions.
* Create diagrams and final rubric.

### Week 6: Final Report

* Write final paper.
* Prepare presentation.
* Package framework and examples.

---

## 19. Initial Bibliography

### Foundational Agent Architectures

1. Yao et al. “ReAct: Synergizing Reasoning and Acting in Language Models.”
2. Schick et al. “Toolformer: Language Models Can Teach Themselves to Use Tools.”
3. Shinn et al. “Reflexion: Language Agents with Verbal Reinforcement Learning.”
4. Yao et al. “Tree of Thoughts: Deliberate Problem Solving with Large Language Models.”
5. Besta et al. “Graph of Thoughts: Solving Elaborate Problems with Large Language Models.”

### Memory and Cognitive Architectures

6. Park et al. “Generative Agents: Interactive Simulacra of Human Behavior.”
7. Wang et al. “Voyager: An Open-Ended Embodied Agent with Large Language Models.”
8. Sumers et al. “Cognitive Architectures for Language Agents.”

### Multi-Agent Systems

9. Wu et al. “AutoGen: Enabling Next-Gen LLM Applications via Multi-Agent Conversation.”
10. Hong et al. “MetaGPT: Meta Programming for a Multi-Agent Collaborative Framework.”
11. Li et al. “A Survey on LLM-based Multi-Agent Systems.”
12. Tran et al. “Multi-Agent Collaboration Mechanisms: A Survey of LLMs.”

### Surveys and Taxonomies

13. Wang et al. “A Survey on Large Language Model based Autonomous Agents.”
14. Xi et al. “The Rise and Potential of Large Language Model Based Agents: A Survey.”
15. Händler. “Balancing Autonomy and Alignment: A Multi-Dimensional Taxonomy for Autonomous LLM-powered Multi-Agent Architectures.”
16. Buyya et al. “Agentic Artificial Intelligence: Architectures, Taxonomies, and Evaluation of Large Language Model Agents.”
17. Alenezi. “The Evolution of Agentic AI Software Architecture.”

### Agent Interfaces and Software Engineering

18. Yang et al. “SWE-agent: Agent-Computer Interfaces Enable Automated Software Engineering.”

---

## 20. Final Project Abstract

Agentic AI systems are commonly evaluated using task success, benchmark performance, latency, and cost. While useful, these metrics do not explain how agentic systems differ architecturally. A single ReAct agent, a planner-executor workflow, a reflection-based agent, and a multi-agent SOP-driven system may all solve similar tasks while having fundamentally different structures. This project proposes a formal parameterization framework for comparing agentic AI architectures independently of task performance. The framework represents an agentic system as an architecture vector covering goal structure, control topology, planning depth, memory model, tool/action model, reflection loops, human oversight, observability, failure recovery, and safety boundaries. The project will survey foundational and recent literature, extract recurring architectural dimensions, define scoring rubrics, and apply the framework to representative systems including ReAct, Toolformer, Reflexion, Tree of Thoughts, Graph of Thoughts, Generative Agents, Voyager, AutoGen, MetaGPT, and SWE-agent. The expected contribution is a reusable architecture-level vocabulary and metric framework for analyzing, comparing, and designing agentic AI systems beyond benchmark performance.
