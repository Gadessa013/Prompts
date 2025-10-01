# AI Agent Prompt Architecture: A Comprehensive Guide (v2.1)

## 1. Project Overview & Philosophy

### 1.1. Overview
This document outlines the re-architecture of the system prompts for a multi-node AI workflow agent. The project's primary goal was to evolve a set of functional but inconsistent original prompts into a robust, professional, and highly reliable system. The prompts for six key nodes were systematically analyzed and refined: Start Conversation, Inform, Ask Details, Decision, Completed, and Create Ticket. The result is a unified, user-centric, and technically precise prompt architecture that ensures consistent behavior and a superior user experience.

### 1.2. Guiding Philosophy
The core philosophy of this project was a shift from a purely technical instruction set to a comprehensive agent behavior model. A successful AI agent requires more than just a list of tasks; it needs a well-defined persona, clear conversational rules, and robust error-handling logic. This approach treats each prompt as a blueprint for a specialized "employee," ensuring each one is a reliable expert at its specific job while still being a consistent representative of the overall brand.

---

## 2. The Core Problem with the Original Prompts
The initial analysis revealed several systemic weaknesses that posed significant risks to reliability and user satisfaction.

* **Inconsistent Structure:** Each prompt was a freeform text file with different heading styles and section orders. This made maintenance difficult and increased the cognitive load for developers.
* **Unprofessional Persona:** The defined "playful with lazy vibes" and use of slang was misaligned with a professional service context, which could erode user trust.
* **Lack of Conversational Logic:** The prompts told the AI what data to get but not how to ask for it, leading to poor user experiences (e.g., asking for all details at once).
* **"Rule Amnesia":** Critical rules, like the trilingual language protocol, were not consistently applied across all nodes. This meant the agent would "forget" rules mid-workflow, creating jarring interactions.

---

## 3. The New, Standardized Prompt Architecture
To solve these problems, a consistent, modular structure was implemented for every prompt. This architecture is the foundation of the agent's improved reliability and predictability.

**Standard Sections & Their Purpose:**

* Master Persona
* Role
* Immediate Goal
* Linguistic Capabilities
* Technical Specifications
* Operational Logic
* Tool Usage Protocol
* Constraints / Common Mistakes to Avoid

---

## 4. Summary of Key Global Changes
Across all nodes, the following critical improvements were made:

* **Unified the Persona:** The inconsistent tone was replaced with a single, professional persona to build user trust and establish a coherent brand identity.
* **Fused Technical & Conversational Instructions:** The core strategy created a hybrid prompt that respects both the needs of the back-end (data formatting) and the front-end (a polite, logical conversation).
* **Prioritized User Experience:** Specific conversational logic was implemented, such as "ask for one piece of information at a time," providing acknowledgments, and validating user input.
* **Ensured Language Consistency:** By adding the Linguistic Capabilities section to every single node, the design guarantees the agent will not break its language rules—a major reliability risk in the original design.

---

## 5. Detailed Node-Specific Refinements

### 5.1. Start Conversation Node
**Core Objective:** To greet the user and immediately determine their primary intent from a predefined list.
**Original Prompt Weaknesses:** The goal was ambiguous, allowing the AI to get drawn into general conversation instead of routing the user. It lacked strict language rules.
**Key Architectural Changes:**
* Defined a precise Immediate Goal: "determine which conversation starter is closest to the user's intent."
* Implemented a "Greet, Match, and Pass" logic, preventing any chit-chat. The agent's only task is to find the intent and call the tool.
* Added the mandatory Linguistic Capabilities section for consistent language handling from the very first message.
**Result:** A highly efficient and predictable Triage Agent that eliminates conversational drift at the start of the workflow.

### 5.2. Inform Node
**Core Objective:** To deliver a specific piece of information while also being able to handle relevant user questions.
**Original Prompt Weaknesses:** The prompt only accounted for pushing information and couldn't handle user queries. It could be easily derailed if the user asked a question.
**Key Architectural Changes:**
* Created a hybrid logic with a Primary Objective (deliver info) and a Secondary Objective (answer questions).
* Implemented an "Answer & Pivot" mechanism, where the agent answers a side-question and then immediately transitions back to its primary goal.
* Added a strong Tool Usage Protocol that requires explicit user confirmation before proceeding.
**Result:** A flexible Information Specialist that can manage user detours without abandoning its core task, making the conversation feel more natural and intelligent.

### 5.3. Ask Details Node
**Core Objective:** To methodically collect multiple pieces of information from the user.
**Original Prompt Weaknesses:** Lacked any conversational strategy, risking the AI asking for all information at once. It also had no data validation instructions.
**Key Architectural Changes:**
* Implemented a strict "One Question at a Time" Operational Logic, which is critical for a good user experience.
* Added a "Listen & Validate" step, instructing the AI to check if the user's response matches the expected data type (e.g., a date) and to clarify if it doesn't.
* Fused the conversational logic with the original's technical requirements, ensuring the AI collects the data politely and submits it to the tool correctly using the proper id for each field.
**Result:** A patient and Methodical Data Gatherer that reduces user frustration and significantly increases the quality of the data collected.

### 5.4. Decision Node
**Core Objective:** To determine the correct workflow path based on a set of logical conditions.
**Original Prompt Weaknesses:** It only accounted for silent, backend decisions and had no logic for when the agent needed to ask the user to make a choice. The reasoning parameter was undefined.
**Key Architectural Changes:**
* Architected a Dual-Mode Logic ("Mode A: Internal Analysis" and "Mode B: User-Facing Choice"), allowing the agent to understand two different ways of making a decision.
* Provided clear triggers and step-by-step instructions for each mode.
* Added instructions on how to formulate the reasoning string for the tool call, improving data logging and debuggability.
**Result:** A sophisticated Workflow Navigator that can handle both automated and user-driven branching logic with precision.

### 5.5. Completed Node
**Core Objective:** To gracefully and definitively end the conversation.
**Original Prompt Weaknesses:** It simply told the AI to "end gracefully" with no strategy. It couldn't handle users who tried to start a new query.
**Key Architectural Changes:**
* Implemented a structured three-step closing process: "Deliver Closing -> Offer Final Assistance -> End Interaction."
* Added a specific constraint with a pre-written script for handling new, complex questions, preventing scope creep.
* Included a critical negative constraint in the Tool Usage Protocol: "You MUST NOT call the continue_workflow tool."
**Result:** A Professional Conversation Closer that provides a clear and polite sense of finality, improving user satisfaction and preventing the agent from getting stuck in conversational loops.

### 5.6. Create Ticket Node
**Core Objective:** To guide the user through the most complex data-gathering task and confirm its success.
**Original Prompt Weaknesses:** It was a long, technical checklist with no conversational flow, risking user confusion. It also lacked a final confirmation step.
**Key Architectural Changes:**
* Structured the data requirements into a clear "Required Information Checklist."
* Designed a sequential Operational Logic that guides the user through the collection process one category at a time (Subject, then Contact Info, etc.).
* Created an advanced Tool Usage Protocol that handles an optional pre-tool call (list_attachments) and, most importantly, instructs the AI to wait for the tool's response and report the final reference number to the user.
**Result:** An expert Ticket Creation Specialist that can manage a complex, multi-step task while keeping the user informed and engaged, and confirming the final outcome of the process.

---

## 6. Future Recommendations
* **Prompt Library & Versioning:** Treat these refined prompts as version 1.0. As they are modified, a versioning system (e.g., Start_Conversation_v1.1) should be used to track changes and roll back if needed.
* **Component Reuse:** The Linguistic Capabilities section is a perfect example of a reusable component. Copy and paste standardized sections to accelerate development and ensure consistency.
* **Ongoing Testing:** Continuously monitor conversations for "Common Mistakes." When a new failure pattern emerges, update the relevant prompt's "Common Mistakes to Avoid" section to proactively prevent it from happening again.