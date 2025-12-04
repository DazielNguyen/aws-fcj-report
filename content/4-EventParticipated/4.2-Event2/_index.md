---
title: "Event 2"
date: "2025-10-03"
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# Learning Notes from "AI-Driven Development Lifecycle: Reinventing Software Engineering"

### Event Objectives

- Understand how AI can **automate and optimize** each stage of the Software Development Lifecycle (SDLC).
- Grasp the philosophy of **AI augmenting humans rather than replacing them** in the application development process.
- Directly observe how **Amazon Q** and other AI tools support developers from ideation, coding, to infrastructure deployment (Infrastructure as Code – IaC).
- Recognize the "**AI-first development**" trend – where AI becomes a natural part of future software development processes.

### Speaker List

- **Mr.Toan Huynh** - PMP, Senior Solutions Architect, AWS
- **Ms.My Nguyen** - Senior Solutions Architect, AWS

### Highlighted Content

#### Challenges in AI-Assisted Programming

The opening section presented **limitations and challenges when integrating AI into programming**:

- AI cannot yet handle projects with complex logic requiring deep understanding of business context.
- Developers **struggle to control details** in generated code if they don't clearly describe objectives and scope.
- Code quality heavily depends on **prompts and context** provided by users.

This is precisely why AI-DLC was created: **to establish a structured process enabling more effective collaboration between AI and humans.**

#### AI in Development – How AI is Changing Software

This section analyzed how **AI is transforming the software industry**:

- AI assists in code generation, technical documentation, API design, and automated testing.
- Developers transition from "code writers" to "AI orchestrators" — coordinators who guide and evaluate outputs.
- Tools like **Amazon Q, GitHub Copilot, ChatGPT for Developers** become **central tools in modern dev team workflows**.

#### Introduction to AI-DLC

**AI-Driven Development Lifecycle (AI-DLC)** is a software development approach with AI collaboration, where each step is designed to **provide AI with specific context and objectives** to generate more accurate results.

**Inception**

1. **Build Context on Existing Codes** – AI is "fed" with current source code to understand project structure.
2. **Elaborate Intent with User Stories** – Developers describe requirements through user stories, clarifying objectives.
3. **Plan with Units of Work** – Break down work into small units for AI to execute and generate code incrementally.

**Construction**

4. **Domain Model (Component Model)** – Build domain models or logical architecture diagrams.
5. **Generate Code & Test** – AI generates code and automated tests based on planned information.
6. **Add Architectural Components** – Add architectural components like APIs, data layers, logging, security.
7. **Deploy with IaC & Tests** – Automatically deploy systems with Infrastructure as Code and integration tests.

_Each step provides additional "rich context" for the next step, helping AI understand the system more deeply and generate increasingly accurate results._

#### CORE CONCEPTS – Three Core Principles

1. **Context Awareness** – AI needs clear context about code, requirements, and domain to operate effectively.
2. **Collaborative Generation** – Humans and AI collaborate: AI generates code, humans guide and review.
3. **Continuous Refinement** – Iterative process to refine outputs and improve quality.

#### Mob Elaboration

Mob Elaboration is a method for expanding requirements (intent elaboration) through team collaboration:

- Multiple members jointly describe requirements, ask questions, and add information for AI.
- Helps AI **understand more deeply** about business, objectives, and complex project logic.
- This approach helps **reduce misunderstanding risks**, especially in large or multi-domain teams.

#### 5-Stage Sequential Process of AI-DLC

AI-DLC is executed through 5 stages:

1. **Inception** – Understand requirements, analyze systems.
2. **Construction** – Create domain models and initial structure.
3. **Generation** – Automatic code generation.
4. **Testing** – Automate unit and integration testing.
5. **Deployment** – Deploy applications with IaC and CI/CD pipelines.

Each iteration helps AI learn more and improve output quality.

#### Demo 1 – Hands-on Experience with AI DLC using Amazon Q

The demo illustrated how to apply AI-DLC in practice through **a small project**:

- Starting from **a simple idea** → converting to **user story** describing business requirements.
- AI assists in **dividing work (Units of Work)** and detailed planning for each module.
- Participants can **control AI through questions, checkboxes, and logical conditions**, helping AI understand the scope of work.
- AI continues to generate code, write tests, create project structure, and automatically deploy trials.
- The demo clearly showed how **AI and humans collaborate harmoniously**: AI handles repetitive tasks, humans guide and make strategic decisions.

#### Introduction to Kiro

**Kiro's Philosophy**

The next part of the workshop introduced **Kiro**, an intelligent development environment designed **around the "AI-native development" philosophy** – where AI is a core component, not just a support tool.

Kiro's philosophy focuses on three main elements:

1. **Deep integration with development processes** – AI not only assists in writing code but also participates in planning, managing context, and analyzing change impacts.
2. **Comprehensive project context understanding** – Kiro maintains continuous state awareness of system structure, allowing AI to interact with the entire project rather than individual files.
3. **Intelligent control & collaboration** – Developers can guide AI through **contextual commands**, ensuring each change has a clear purpose and is consistent with the system.

**Project Structure in Kiro**

Unlike **traditional text editors** like VSCode or JetBrains, Kiro is not just a code writing environment — it's an **AI workspace with structural awareness**.

Project structure in Kiro includes:

- **Context Layer** – Stores context, domain models, and relationships between modules.
- **Task Layer** – Manages Units of Work tracked and gradually completed by AI.
- **AI Agent Layer** – Each task (code, test, refactor, deploy) has a dedicated agent, creating a **multi-agent – collaborative – parallel** development model.
- **Human-in-the-Loop Control** – Developers can intervene at every step: confirm, modify, or reject AI outputs.

This makes Kiro not just a code generation tool but **a collaborative development ecosystem between humans and AI**.

#### Demo 2: Kiro – Applying AI-DLC

In the demonstration, the speaker illustrated how Kiro operates **AI-DLC seamlessly**:

1. User inputs **a basic business requirement**, e.g., "build an event management system".
2. Kiro automatically analyzes intent, creates domain models, and breaks down into user stories.
3. AI in Kiro generates **corresponding modules, components, and test cases**.
4. Developers can interact through **checkbox-based task control** to confirm each part of the work.
5. Finally, Kiro **deploys the complete system** with IaC and automated testing.

The demo showed that **AI-DLC is not just theory**, but can **be implemented practically within the Kiro environment** — where AI, humans, and development processes merge into a unified system.

### Event Experience

Participating in the **"AI DLC x Kiro: Reinventing Developer Experience with AI"** workshop was an extremely valuable experience, helping me better understand how **AI is deeply integrated into software development environments** and how **Kiro's design philosophy** brings a new approach to developers.

#### Learning from Expert Speakers

- Speakers shared about **AI DLC** – a platform supporting AI-based software development, automating many SDLC processes.
- Additionally, the introduction to **Kiro Editor** provided deep insights into building a text editor in an **AI-native** direction rather than just "adding AI plugins" to old environments.
- I was particularly impressed with Kiro's philosophy: **minimalist, high-performance, focused on user experience and module-based scalability**.

#### Practical Technical Experience

**In learning:**

- Apply AI-DLC structure for personal projects
- Practice "Context Awareness" principle with AI assistants
- Build habit of writing clear requirements as user stories

**For future career:**

- Understand modular, extensible, maintainable system design like Kiro
- Master Amazon Q and other AI tools effectively
- Recognize importance of providing quality context for AI

**Mindset shift:**

- Approach problems with "AI-augmented" thinking
- Consider building custom tools with deep AI integration
- Always ask: "How can AI assist better at this step?"

#### Applying Modern Tools

- Experiencing **AI DLC on Kiro** helped me better understand the capability of **automating development processes**, especially in steps like code generation, documentation, and debugging.
- I recognized the potential of **building personal learning and working tools** with intelligent suggestions, helping shorten development time and improve product quality.
- Kiro's modular design concepts also suggested directions for **designing flexible, scalable, and maintainable systems**.

#### Networking and Exchange

- The workshop created opportunities for me to **connect with developers, AI researchers, and product designers**, thereby learning more about the **AI-augmented development** trend.
- Through discussions, I learned much about how **AI can play the role of creative collaborator**, helping developers focus more on logic and system thinking rather than repetitive operations.

#### Lessons Learned

Participating in the **"AI DLC x Kiro"** workshop was a turning point in how I perceive AI's role in software development.

**The most important thing** I learned wasn't specific tools, but the necessary **mindset shift**:

- AI is not a tool for faster coding
- AI is a partner for better thinking and system design
- Structured processes (like AI-DLC) are more important than raw AI power

The workshop also showed me the future of development tools - where **AI-first architecture** like Kiro will become standard, and developers need to prepare for this paradigm shift.

Insights from AWS Solution Architects and hands-on experience with Kiro equipped me with a solid foundation to apply AI in my learning journey and future career in software engineering.

#### Some Photos from the Event

<img src="/images/4-EventParticipated/4.2-Event2/Event_02_IMG_6887.png" alt="Event_02" width="2000"/>

> **Group photo check-in after the event**

> This is the group check-in moment after the workshop ended. This event provided many valuable insights about how AI is reshaping development workflow.

<img src="/images/4-EventParticipated/4.2-Event2/Event_02_IMG_6884.jpeg" alt="Event_02" width="2000"/>

> **Professional event space**

> The workshop was professionally organized with complete demo stations and networking opportunities. This was one of the important events that helped me deeply understand AI-driven development.
