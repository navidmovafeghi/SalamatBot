# ADD

- **STEP 1:**
    
    **Define Core Vision, Features & "-ilities" (Original Phase 0)**
    
    - **Action:** Get stakeholder and team alignment on the project's purpose, core features, and, most importantly, the top 3-5 prioritized **architecture characteristics**
    - **Output:** A clear mission statement and a prioritized list of "-ilities". This is your north star.
    
    ---
    
    **OUTPUT:**
    
    **Project Mission:** To become the most trusted and user-friendly digital health companion for Persian speakers, reducing health anxiety and combating misinformation.
    
    ---
    
    **Core Features:**
    
    - **Conversational Medical Inquiry:** The core of the product is an AI-powered chat interface where users can ask general medical questions in natural Persian and receive safe, reliable, and context-aware answers.
    - **Proactive Health Management:** The product will provide tools that help users actively manage their health, such as setting reminders for medications and appointments. This functionality moves the user from a reactive to a proactive state.
    - **Consolidated Personal Health Record:** Users must have a secure, private place to record and track their key health metrics over time (e.g., blood pressure, blood glucose).
    - **Secure Account & Subscription Management:** The product will provide robust functionality for users to manage their accounts, privacy settings, and subscription status seamlessly.
    
    ---
    
    **Core Non-Functional Requirements (NFRs):**
    
    - **a. Reliability & Availability:**
        - The service must maintain an uptime of **99.9% ("three nines")**. Users, especially paying ones, depend on us to be available.
        - Data integrity is paramount. User health records and subscription data must never be corrupted or lost. Regular, automated backups are required.
    - **b. Performance & Scalability:**
        - Chatbot responses should feel instantaneous. The goal for average response time (p50) is **under 3 seconds**.
    - **d. Usability & Accessibility:**
        - The user interface must be **simple, intuitive, and calming**, especially for non-technical users or those in a state of anxiety.
        - The language used throughout the application must be clear, empathetic, and easily understandable.
    - **e. Maintainability & Extensibility (For the Developer):**
        - The codebase must be clean, well-documented, and organized.
        - The architecture must be modular, allowing for new features (Epics) to be added without requiring a complete rewrite of existing, stable components

---

- **STEP 2:**
    
    **Establish High-Level Structure** 
    
    - **Action (Partitioning):** Choose your top-level partitioning strategy (e.g., Domain-Partitioning). Define the primary, coarse-grained modules or services (e.g., UserService, OrderService, InventoryService).
    - **Action (Style):** Select the overarching architectural style (e.g., Modular Monolith, Microservices).
    - **Output:**
        - Result of the decision on partitioning strategy and if it is domain partitioning define the domains
        - Result of the desicion on the architectural style
    
    ---
    
    **OUTPUT:**
    
    **Architectural Style: Modular Monolith**
    
    - **Rationale:** This style provides the best balance for SALAMATBOT's goals. It offers development and deployment simplicity in the early stages while enforcing strong internal boundaries. This directly supports **Maintainability** and creates a clear path for future **Extensibility** (e.g., spinning off a module into a microservice if needed) without the high initial operational overhead of a distributed system.
    
    **Top-Level Partitioning Strategy: Domain Partitioning**
    
    - **Rationale:** The system is partitioned into logically distinct business domains. This aligns the code structure with the business vision, reduces cognitive load for developers, and enables teams to work on different domains (e.g., Health Management, Billing) with minimal interference.
    - **Defined Core Domains (Modules)**
        
        Here are the primary domains for SALAMATBOT. Each will be a distinct module within the monolith, with its own data schema and a well-defined public API for communicating with other modules.
        
        1. **Identity & Access Module:**
            - **Responsibility:** Handles everything related to the user as a person. User registration, login/logout, profile management (name, etc.), password resets, and issuing authentication tokens (JWTs).
            - **PRD Justification:** Directly supports the "Secure Account & Subscription Management" principle. It is the foundation for all user-specific activity.
        2. **Inquiry & AI Module:**
            - **Responsibility:** The core chatbot functionality. Manages conversational state, sanitizes user input, interfaces with the external Large Language Model (LLM), enforces safety guardrails (like adding disclaimers), and logs conversation history for analytics and safety audits.
            - **PRD Justification:** Implements the "Conversational Medical Inquiry" core feature. This is the primary value proposition for the "Worried Well" persona (Sara).
        3. **Billing & Subscriptions Module:**
            - **Responsibility:** Manages all financial aspects. Integrates with the payment gateway, handles subscription plans (freemium logic, 10-question limit), processes payments, and manages the subscription lifecycle (active, canceled, trialing).
            - **PRD Justification:** Implements the business model and the "Monetization" phase. It is a distinct and critical domain that should not be entangled with user identity or health data.
        4. **Personal Health Record (PHR) Module:**
            - **Responsibility:** Securely stores and manages sensitive, user-entered health data (e.g., blood pressure logs, glucose levels). It will have the strictest access control rules in the entire system.
            - **PRD Justification:** Implements the "Consolidated Personal Health Record" feature, a key part of the "Health Management Suite" (Phase 3). Separating it isolates sensitive PHI data.
        5. **Health Management Module:**
            - **Responsibility:** Manages proactive health tools. This includes the logic for creating and triggering medication reminders and appointment reminders via background jobs.
            - **PRD Justification:** Implements the "Proactive Health Management" feature, directly addressing the pain points of the "Caregiver" persona (Reza) and increasing product stickiness (Phase 3).

---

- **STEP 3:**
    
    ### Cross-Cutting Concerns
    
    - **Security:**
        - **Authentication:** JWTs will be issued by the Auth Service upon login and validated at the API Gateway for every protected request.
        - **Authorization:** The API Gateway performs a coarse-grained check (is the user logged in?). Each service (PHR Service, Subscription Service) performs fine-grained checks (does this user have permission to access *this specific record*?).
        - **Data Protection:** PHI/PII will be encrypted at rest in the database and always in transit (TLS 1.2+).
    - **Logging:** Centralized, structured JSON logging will be used. Every log entry will contain a correlation_id to trace a single request as it flows through multiple components.
    - **Configuration:** A unified configuration service/strategy will be used, loading settings from environment variables to conform to 12-factor app principles.
    - **Internationalization (i18n):**
        - **Rationale:** This is a mission-critical concern, directly supporting the core vision of serving **Persian speakers**. It is fundamental to the **Usability & Accessibility** NFR, ensuring the application feels native, trustworthy, and empathetic.
        - **Implementation:**
            1. **Right-to-Left (RTL) First:** The frontend architecture will be built with RTL support as a primary requirement, not an afterthought. This means using CSS logical properties (e.g., padding-inline-start instead of padding-left) and selecting component libraries with proven RTL compatibility.
            2. **Resource Files:** All user-facing strings (UI labels, error messages, static content) will be managed in locale-based resource files (e.g., fa.json). The application will load the appropriate strings based on user preference or browser settings.
            3. **Language Scope:** The initial and primary language is **Persian (fa)**. However, the system's design will be language-agnostic from day one, allowing for the future addition of English (en) or other languages without requiring architectural changes, thus supporting **Extensibility**.
    - **Caching Strategy:**
        - **Rationale:** To meet the aggressive **Performance** NFR of sub-3-second responses and to improve **Reliability** and cost-efficiency by reducing load on expensive downstream services (like the LLM API) and the primary database.
        - **Implementation:** A multi-layered caching approach will be employed.
            1. **Distributed Cache (Redis):** A shared Redis instance will be the primary caching layer. It is crucial for maintaining state and performance if the monolith needs to be scaled horizontally (run on multiple servers).
            2. **Primary Targets for Caching:**
                - **LLM Responses:** Common, non-personalized medical inquiries (e.g., "what are symptoms of the common cold?") will be cached to avoid repeated, expensive API calls to the LLM. A Time-To-Live (TTL) of several hours will be used.
                - **User Session & Subscription Data:** Key user details (ID, subscription status, question count) will be cached to avoid database queries on every authenticated request. This data will have a shorter TTL and will be invalidated upon events like subscription changes or logout.
                - **Hot Path Health Data:** While most PHR data will be fetched directly for security and freshness, aggregated data for dashboards or frequently viewed metrics may be cached with very short TTLs.

---

- ***STEP 4:***
    
    **Create Diagrams For The Project**
    
    - **Action (C4 Model):** Create C1 and C2 base diagrams for the project in structurizr
    - **Action (Interaction):** Sketch a high-level component diagram (C1 Context or C2 Container Diagram). Show how the major pieces will generally communicate (e.g., "In-process calls for the monolith," "Asynchronous events between Service A and B").
    - **Output:**
        - a dsl file for the project

---

- ***STEP 5:***
    
    **Finalize Foundational Technology Stack**
    
    - **Action:** Select a coherent set of technologies that directly support the architectural style and NFRs.
    - **Output:** A "Technology Stack" section in the ADD.
    
    ---
    
    **OUTPUT:**
    
    ### **Technology Stack**
    
    This stack is chosen to maximize solo developer productivity while strictly adhering to the project's core NFRs, especially **Maintainability**, **Extensibility**, and **i18n Support**.
    
    - **Backend (Modular Monolith):**
        - **Language:** **TypeScript**. Enforces strong typing for maintainability and clear contracts between modules.
        - **Framework:** **NestJS**. Chosen for its first-class support for modular architecture, which directly implements our Domain Partitioning strategy. Its dependency injection system helps enforce boundaries.
        - **Database ORM:** **Prisma**. Selected for its superior developer experience and strong TypeScript integration, ensuring data access is safe and efficient.
        - **Background Jobs:** **BullMQ**. A robust, Redis-backed queue system for handling asynchronous tasks like medication reminders in the Health Management module.
    - **Database & Cache:**
        - **Primary Database:** **PostgreSQL**. For its proven reliability, transactional integrity (critical for Billing & PHR), and powerful features like JSONB and `pgcrypto`.
        - **Cache / Broker:** **Redis**. To implement the multi-layered caching strategy and to serve as the message broker for BullMQ.
    - **Frontend:**
        - **Framework:** **Next.js (React)**. For its excellent performance (SSR), built-in i18n/RTL support (critical for Persian), and overall developer productivity.
        - **UI Library:** **TBD**
        - **Server State:** **React Query (TanStack Query)**. To manage data fetching, caching, and synchronization with the backend, reducing boilerplate and improving perceived performance.
    - **Infrastructure & DevOps:**
        - **Containerization:** **Docker & Docker Compose**. To create a consistent and reproducible development and production environment for all services (backend, database, cache).
        - **Deployment:** A PaaS-first approach.
            - **Frontend:** **Vercel**. For seamless, zero-config deployment of the Next.js application.
            - **Backend & Database:** **Railway** or [**Fly.io**](http://fly.io/). For easy deployment and management of the Dockerized NestJS monolith, PostgreSQL, and Redis.

---

- **ADRS**
    
    ### **ADR-001: Modular Monolith vs. Microservices**
    
    - **Status:** Decided
    - **Context:** We are an early-stage product (SALAMATBOT) with a clear, phased roadmap. Our primary NFRs are **Maintainability** and **Extensibility**, but our immediate business need is speed to market to validate the product and business model (Phase 1 & 2).
    - **Decision:** We will build SALAMATBOT as a **Modular Monolith**. The application will be a single deployable unit, but the codebase will be partitioned into the strict, independent domains listed above (Identity, Inquiry, Billing, etc.). Communication between modules will be handled via a lightweight, in-process event bus or mediator pattern, not direct method calls, to enforce decoupling.
    - **Consequences:**
        - **Positive:**
            - **Faster Development:** Single codebase and IDE makes initial feature development and refactoring faster.
            - **Simplified Deployment:** One service to deploy, manage, and scale initially. Reduces operational complexity.
            - **No Network Latency:** In-process communication between modules is orders of magnitude faster than network calls in a microservices architecture.
            - **Clear Extensibility Path:** If a module (e.g., the Inquiry & AI Module) requires independent scaling or a different tech stack later, its strong boundaries make it a prime candidate to be extracted into a separate microservice.
        - **Negative:**
            - **Shared Release Cycle:** All modules are deployed together. A change in the Billing module requires a full redeployment.
            - **Risk of Boundary Erosion:** The team must be disciplined to prevent modules from becoming tightly coupled over time.
            - **Technology Stack Homogeneity:** All modules must be written in the same language/framework.

---

- **STEP 5:**
    
    **Risk Assessment & Mitigation Plan**
    
    - **Action:** Document known technical and product risks, their potential impact, and the proactive strategies in place to mitigate them.
    - **Output:** A "Risk Assessment" section added to the ADD.
    
    ---
    
    **OUTPUT:**
    
    ### **Risk Assessment & Mitigation**
    
    This section identifies the most critical risks to the SALAMATBOT project and outlines the architectural, technical, and process-oriented strategies designed to mitigate them.
    
    ### **Product Safety & User Trust**
    
    The most critical risk to the project is **LLM Hallucination & Harmful Advice (RISK-01)**. Given the high likelihood of AI models producing plausible but incorrect information, a failure here could cause direct user harm and would be an existential threat to the product's mission. The mitigation strategy is a multi-layered defense. Firstly, we will use **Retrieval-Augmented Generation (RAG)** to ground all responses in a curated, trusted knowledge base, minimizing reliance on the LLM's general knowledge. Secondly, **systemic disclaimers** will be embedded in the UI to constantly remind users that the service is not a substitute for professional medical advice. Thirdly, the `Inquiry & AI Module` will contain **output guardrails** to filter and block responses containing dangerous keywords or patterns. Finally, the user feedback loop ("👍 / 👎") is a core safety feature to rapidly identify and remediate inaccurate responses.
    
    ### **Security & Data Privacy**
    
    A **Breach of Personal Health Records (PHR) (RISK-02)** is another critical risk. The project will handle sensitive PHI, making security paramount. Our mitigation strategy follows a "Defense in Depth" approach. Architecturally, the `PHR Module` is **isolated as a distinct domain** with the strictest access controls. Technically, all sensitive PHI/PII will be **encrypted at rest** in the PostgreSQL database (using `pgcrypto`) and always encrypted **in transit** (TLS 1.2+). At the application level, we will implement **fine-grained, record-level authorization checks** to ensure a user can only access their own data, preventing Insecure Direct Object Reference (IDOR) vulnerabilities as per OWASP best practices.
    
    ### **Architecture & Technical Debt**
    
    The primary architectural challenge is **Monolith Boundary Erosion (RISK-03)**. As a high-impact, high-likelihood risk, it could degrade the codebase into a "Big Ball of Mud," violating our core `Maintainability` NFR. The primary technical mitigation is the choice of **NestJS**, whose `Module` system is designed to enforce domain separation. This is complemented by a process-level mitigation: inter-module communication must use a **decoupled pattern** (like an in-process event bus), forbidding direct method calls across domain boundaries. This is reinforced by the "Analysis & Design Day" in our development workflow, which forces deliberate consideration of these boundaries for every new feature.
    
    ### **Performance & External Dependencies**
    
    Meeting our performance NFRs involves two key risks. First is **Slow AI Responses (RISK-04)**, where latency from the LLM provider could violate the sub-3-second response time goal. This will be mitigated with an **aggressive Redis caching layer** for common queries, bypassing the LLM entirely. We will also select LLM models optimized for speed and use asynchronous UI patterns (e.g., "thinking..." indicators) to manage user perception.
    
    Second is **LLM Provider Lock-in (RISK-05)**. Becoming dependent on a single provider that becomes too expensive or unreliable is a high-impact risk. To mitigate this, the `Inquiry & AI Module` will be built using an **Adapter Pattern**. It will interact with a generic `LLMAdapter` interface, not a specific provider's SDK. This architectural abstraction will allow us to swap the underlying LLM provider (e.g., from OpenAI to Gemini) by simply implementing a new adapter, without requiring a rewrite of the core business logic.
    
    ### **Operational Risks**
    
    As a solo-developer project, the **Solo Developer Bottleneck (RISK-06)** is a constant, high-impact risk. Burnout or illness could halt progress entirely. Mitigation focuses on maximizing productivity and reducing cognitive load. We will heavily rely on **managed PaaS solutions** (Vercel, Railway/Fly.io) to abstract away infrastructure complexity. The **high-productivity technology stack** (NestJS, Next.js, Prisma) was chosen specifically to minimize boilerplate. Finally, the structured `Workflow.md` provides a sustainable, predictable rhythm to ensure consistent progress without leading to burnout.
    

---