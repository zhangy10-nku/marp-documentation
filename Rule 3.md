# **Rule 3: Ship Early, Learn Fast, Users Are Your North Star**

**MVP ASAP. Talk with users often. Get feedback as soon as possible.**

---

## Table of Contents

1. [Core Principles](#core-principles)
2. [Understanding Your Users](#understanding-your-users)
3. [Iterative Development: Build, Measure, Learn](#iterative-development-build-measure-learn)
4. [Balancing Architecture and Speed: Evolutionary Design](#balancing-architecture-and-speed-evolutionary-design)
5. [Common Pitfalls Engineers Must Avoid](#common-pitfalls-engineers-must-avoid)

---

## Core Principles

Get a Minimum Viable Product into users' hands as quickly as possible. Real-world feedback beats theoretical planning every time. Your users define success—regular communication ensures you're building what actually matters. Quick feedback loops and genuine understanding of user needs prevent wasted effort and missed opportunities. Iterate based on actual usage, not assumptions.

**Avoid over-engineering based on current information.** Your knowledge of the project is everchanging and constantly growing, and so are your requirements. The project grows just as the users you support grow—they learn, they improve processes, and with it, your project and you both need to adapt.

---

## Understanding Your Users

It is critical to learn the users' business just as much as you learn your own. Spend as much time learning business knowledge and use cases as you would learning a new tech stack. You need to master the use cases to the point where you are a power user of your own software. This deep understanding prevents building elaborate solutions for problems that don't exist while ensuring you address the real challenges users face.

---

## Iterative Development: Build, Measure, Learn

The core principle of user-driven development follows the **Build-Measure-Learn feedback loop** popularized by Lean Startup methodology. This isn't about building throwaway code—it's about building the right thing incrementally.

### Development Practices

**Start with the Simplest Thing That Could Possibly Work (STCPW).** Your first version should be the absolute minimum needed to validate core assumptions. Not the minimum *viable* product, but the minimum *testable* product. Can you solve the user's problem with a manual process before automating? Can you use existing tools before building custom solutions? Can you handle 10 users before optimizing for 10,000? Every feature you don't build is time saved for learning what actually matters.

**Embrace the "You Aren't Gonna Need It" (YAGNI) principle.** Don't build for hypothetical future requirements. Don't add flexibility "just in case." Don't create abstractions before you have at least three concrete use cases that need them. Premature abstraction and premature optimization are the root of much wasted engineering effort. Build for today's known requirements with clean, simple code that will be easy to change tomorrow when you know more.

**Practice Continuous Deployment and Feature Flags.** Decouple deployment from release. Get your code into production frequently—daily or multiple times per day when possible. Use feature flags to control which users see new functionality, allowing you to release to 5% of users, gather feedback, iterate, and gradually roll out. This reduces risk, enables A/B testing, and creates tight feedback cycles. The longer code sits undeployed, the more assumptions remain unvalidated.

**Measure what matters, not what's easy.** Instrument your application to understand actual usage patterns. Which features are users engaging with? Where do they get stuck? What workflows take longer than expected? Use both quantitative metrics (analytics, performance monitoring, error rates) and qualitative feedback (user interviews, support tickets, session recordings). The combination tells you not just *what* users do, but *why* they do it.

**Refactor based on evidence, not speculation.** When user feedback or usage data reveals problems, refactor ruthlessly. When you discover patterns emerging from three similar implementations, now is the time to abstract. When performance metrics show actual bottlenecks affecting real users, now is the time to optimize. Evidence-driven refactoring means you're improving things that matter rather than gold-plating things that don't.

**Version your learning, not just your code.** Each iteration should answer specific questions: Did this feature solve the user's problem? Did they use it the way we expected? What new needs emerged? Document what you learned, not just what you built. Your roadmap should evolve based on validated learning. Be willing to pivot or even remove features that aren't delivering value—there's no shame in deprecating work that taught you what users don't need.

**Maintain architectural flexibility through good design.** This seems contradictory to YAGNI, but it's not—there's a difference between speculative features and sound architectural principles. Write modular, loosely-coupled code with clear interfaces. Follow SOLID principles. Keep business logic separate from infrastructure concerns. This isn't about building for unknown futures; it's about making your current code easy to change when you learn more. Good architecture is what allows you to iterate quickly without accumulating crushing technical debt.

**Set explicit success criteria before building.** Before starting any feature, define what success looks like: What user behavior change do we expect? What metrics will move? What feedback are we hoping to hear? Without this, you can't measure whether an iteration succeeded. This also prevents scope creep—if it's not needed to test your hypothesis, defer it to a future iteration.

**Build in small batches.** Break work into the smallest deployable increments. Instead of building an entire workflow end-to-end, build one step, deploy it, see how users interact with it, then build the next step. Small batches mean faster feedback, easier debugging, simpler code reviews, and less waste when you need to change direction. They also compound the benefits of continuous deployment.

---

## Balancing Architecture and Speed: Evolutionary Design

A critical misconception about iterative development is that it means hacking together solutions without architectural thinking. Nothing could be further from the truth. Fast iteration requires *good* architecture—but it's architecture that emerges and evolves rather than being fully specified upfront. This is **Evolutionary Design**, a principle from Extreme Programming that balances the need for speed with the need for sustainability.

### Architectural Principles

**Invest in foundational architecture decisions early.** Some decisions are expensive to change later and should be made thoughtfully upfront: your data storage strategy, authentication model, core domain boundaries, deployment infrastructure, and API contracts. These are load-bearing decisions that enable or constrain everything built on top. Don't overthink them, but don't ignore them either. Use time-boxed spikes to explore options, consult with experienced engineers, and make informed decisions based on known constraints. Document your reasoning—future you will thank present you.

**Apply the "Rule of Three" for abstractions.** When you implement something once, write concrete code. When you implement it a second time, duplicate with slight variations—resist the urge to abstract. When you implement it a third time, *now* you have enough information to create the right abstraction. This prevents premature abstraction (building the wrong abstraction) while ensuring you don't accumulate infinite duplication. Three concrete examples reveal the actual patterns worth abstracting. As Sandi Metz says: "Duplication is far cheaper than the wrong abstraction."

**Design for replaceability, not reusability.** Instead of trying to build components that anticipate every future use case, build components that are easy to replace when requirements change. Small, focused modules with clear interfaces and minimal dependencies can be swapped out without destabilizing the system. Replaceability gives you options—you can evolve or replace components as you learn more about what's actually needed. This is more valuable than speculative flexibility that may never be used.

**Use architectural fitness functions to prevent decay.** Automated tests aren't just for functionality—they're for architecture too. Create tests that enforce architectural constraints: dependency rules, performance budgets, API contract adherence, security policies. These "fitness functions" provide guard rails that let you move fast without breaking architectural principles. They catch violations early, making technical debt visible before it compounds. If your architecture says "services shouldn't directly access other services' databases," write a test that fails if someone does it.

**Refactor continuously as part of normal work.** Don't wait for dedicated "refactoring sprints"—they rarely happen and they silo improvement work. Follow the Boy Scout Rule: leave code better than you found it. When adding a feature, improve the area you're working in. When fixing a bug, improve the design around it. Small, continuous refactoring prevents the big rewrites that stop all feature development. Budget 15-20% of every sprint for technical improvement work—not as a separate track, but woven into feature delivery.

**Separate stable from volatile concerns.** Some parts of your system change frequently (UI, workflows, business rules), while others remain stable (data models, core algorithms, integration points). Use architectural patterns like Hexagonal Architecture or Clean Architecture to isolate volatile concerns from stable ones. Put stable code at the center, surround it with abstractions (ports), and keep volatile implementations (adapters) at the edges. This allows UI frameworks or third-party integrations to change without touching business logic.

**Embrace the "Strangler Fig" pattern for risky changes.** When you need to replace a significant component but can't afford to rewrite everything at once, use the Strangler Fig pattern: build the new functionality alongside the old, gradually route traffic to the new system, and eventually decommission the old one. This reduces risk, enables incremental validation, and keeps you shipping value while improving architecture. It's how you evolve architecture in production without "big bang" migrations.

**Make reversible decisions reversible, irreversible decisions carefully.** Jeff Bezos distinguishes between Type 1 (irreversible) and Type 2 (reversible) decisions. Type 2 decisions should be made quickly by small teams—if you're wrong, you can undo it. Type 1 decisions deserve more analysis and stakeholder input because they're expensive to reverse. Most decisions are Type 2 but get treated like Type 1, slowing everything down. Be honest about which type you're facing and calibrate your process accordingly.

**Document architectural decisions, not just architecture.** Use Architecture Decision Records (ADRs) to capture *why* decisions were made, what alternatives were considered, and what trade-offs were accepted. When you inevitably need to revisit a decision, this context prevents you from repeating past mistakes or undoing good decisions for bad reasons. ADRs are lightweight—a few paragraphs per decision—but invaluable for maintaining institutional knowledge as the team evolves.

**Measure and manage technical debt explicitly.** Not all technical debt is bad—sometimes taking shortcuts to ship faster is the right trade-off. The problem is *unmanaged* debt that accumulates invisibly. Track debt explicitly: tag TODOs with context, maintain a technical debt backlog, measure code quality metrics over time. Most importantly, make debt visible to product stakeholders so they can participate in prioritization decisions. "We can ship this feature in two weeks with some technical debt, or four weeks with a cleaner implementation" is a business decision, not just a technical one.

### The Key Insight

**Good architecture enables speed.** Architecture isn't opposed to rapid iteration—it's what makes rapid iteration sustainable. Without good architecture, your velocity decreases over time as complexity compounds. With evolutionary design, you maintain the ability to change direction quickly because your system is designed to be changed. You're not planning for every hypothetical future; you're building a system that can adapt to whatever future actually arrives.

---

## Common Pitfalls Engineers Must Avoid

### Product Usage and Testing

**Don't be the engineer who never uses their own product like an end user.** Too many engineers test code in isolation, run a few unit tests, and call it done—never experiencing the full user journey. They don't click through the UI flows, don't try the edge cases real users encounter, and don't feel the pain of poor performance or confusing workflows. If you're not regularly using your software the way your users do, you're building blind.

**Don't think like an engineer—think like an end user.** Engineers often test the "happy path" and a couple of error scenarios, then declare victory. They don't consider the workflows users actually perform, the context in which features are used, or the cumulative friction of small annoyances. They shirk ownership by treating their work as a task to complete rather than a user problem to solve. Real ownership means understanding the why behind the what, anticipating how users will actually interact with your feature, and caring about the complete experience, not just whether your code compiles.

### Knowledge and Collaboration

**Don't become siloed in one corner of the codebase.** Many engineers find their comfort zone—a particular service, module, or technology—and never venture beyond it. They perfect their little domain while the rest of the system remains a mystery. This creates knowledge bottlenecks, limits your ability to see system-wide issues, and prevents you from understanding how your code impacts the broader user experience. Challenge yourself to learn different parts of the system, understand the full stack, and see how everything connects.

**Don't wait for product owners to relay requirements from users.** Too many engineers treat product managers as intermediaries who will handle all user interaction. While product managers own the product vision and point the long-term course for the project, good engineers recognize that project success depends on the buy-in of the individual engineer. You are responsible for meeting with end users directly, gathering opinions, understanding their workflows and pain points, and garnering feedback early and often. Waiting passively for filtered requirements creates a game of telephone where critical context is lost. Own your relationship with users—their insights will make you a better engineer and your work more impactful.

### Requirements and Ownership

**Don't treat requirements as a checklist for bare minimum compliance.** Too many engineers look at a requirement sheet, implement exactly what's written (or less), and move on. They don't ask why the requirement exists, what problem it's solving, or whether the proposed solution actually addresses the user's need. They don't suggest improvements, don't think about edge cases the spec missed, and don't consider the long-term implications. Great engineers engage with requirements critically—they understand the underlying need, propose better solutions when appropriate, and deliver work that solves the actual problem, not just the documented specification.





