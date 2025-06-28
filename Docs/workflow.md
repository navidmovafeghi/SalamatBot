# workflow

### **The Solo Developer's Professional Software Workflow (v4.0 - Streamlined)**

This document is a reusable template for initiating and developing a software project as a solo developer. It emphasizes a professional, structured approach that includes formal analysis and design in every development cycle to ensure quality, maintainability, and a consistent rhythm from concept to delivery.

---

### **Phase I: Foundation & Setup (The "Sprint Zero")**

**Goal:** Establish a professional, automated development environment and a clear architectural blueprint *before* writing the first feature.

**0.[** ✅ **] PRD**

- **Artifact:** PRD.md
- **Output**:
    
    [PRD ](PRD%2021bd12c0b70b809381dbc3a68fc26795.md)
    

**1. [** ✅ **]  Architectural Baseline**

- **Artifact:** ADD.md (in your Git repo)
- **Action:** Document high-level architectural decisions (Core Purpose, -ilities, Style, etc.).
- **Output:**
    
    [ADD](ADD%2021cd12c0b70b802aa93ac52745b65f73.md)
    

**2. [** ✅ **] Finalize Foundational Technology Stack**

- **Action:** Add a "Technology Stack" section to ADD.md.
- **Guideline:** Be deliberate. Choose technologies you know well or have a specific reason to learn.

**3. [** ✅ **] Define Initial Definition of Done (DoD)**

- **Artifact:** DEFINITION_OF_DONE.md (in your Git repo)
- **Action:** Create a minimal, realistic quality checklist that will evolve as you learn.
- **Initial DoD Template:**
    
    ```
    ✅ Code compiles and runs without errors
    ✅ Basic manual testing completed
    ✅ Code committed to version control with clear commit message
    ✅ No obvious bugs or console errors
    ✅ Basic error handling implemented
    ✅ Code follows project naming conventions
    Note: This DoD will evolve as the project matures.
    Last updated: [Date]
    ```
    

**4. [** ✅ **] Risk Assessment & Mitigation Plan**

- **Action:** Document known technical risks and fallback approaches.
- **Artifact:** Add "Risk Assessment" section to ARCHITECTURE.md.

**5. [ ] Environment & Pipeline Setup**

- **Action:** Build the practical infrastructure for development.
- **Checklist:** Source Control, Project Scaffolding, Code Quality Tools, Environment Variables, Developer Experience (DX), Database Setup, Basic CI Pipeline, "Smoke Test" Verification.

**6. [ ] Performance & Security Baseline**

- **Action:** Define basic performance requirements and security standards.
- **Artifact:** Add sections to ARCHITECTURE.md for performance targets and security considerations.

**7. [ ] Create the Initial Product Backlog**

- **Action:** Set up your project board (e.g., GitHub Projects).
- **Checklist:**
    - **Configure Board:** Create columns: Backlog, **Sprint Ready**, **This Sprint**, In Progress, Done.
    - **Configure Labels:** Create labels like Epic, User Story, Bug, Chore, Spike, Technical Debt.
    - **Create Epics:** Create issues for high-level feature sets.
    - **Write Initial Stories:** Create issues for the first few stories with basic user story format (As a... I want... So that...). **Note:** Acceptance Criteria will be added during Backlog Refinement.

---

### **Phase II: Iterative Development (The Sprints)**

**Goal:** Build the application incrementally with a consistent rhythm that formally separates design from implementation, with evolving quality standards.

**The Weekly Rhythm (Example: 1-Week Sprint)**

**Monday: Analysis & Design Day (The "Architect & Analyst Hat")**

- **Morning (1 hour) - Sprint Planning:**
    1. **Declare Sprint Goal:** State a clear, achievable goal. e.g., "This week, I will fully design, build, and test the User Registration feature."
    2. **Select Work:** Move the highest-priority User Story from the Sprint Ready column to the This Sprint column. This is the focus for the week.
- **Afternoon (2-3 hours) - Deep Analysis & Design Session:**
    
    **Goal:** Transform a user story into a complete technical blueprint that makes implementation almost mechanical.
    
    **Pre-Design Setup (10 minutes)**
    
    ```markdown
    ## Pre-Design Checklist
    - [ ] DoD reviewed and updated for this story's complexity
    - [ ] Story-specific quality requirements identified
    - [ ] All acceptance criteria are clear and testable
    - [ ] Dependencies identified and available
    - [ ] Architecture patterns for this feature decided
    
    ```
    
    **Phase 1: System Context & Input Analysis (15 minutes)**
    
    - **Input Gathering:** Re-read user story, acceptance criteria, business & technical context
    - **System Integration Mapping:** Document existing components affected, new components needed, integration points, architectural patterns
    
    **Phase 2: Happy Path Design (30 minutes)**
    
    - **Step 1:** Walk through successful user interaction narrative
    - **Step 2:** Create sequence diagram in Mermaid syntax for technical flow visualization
    
    **Phase 3: Data Contract Design (20 minutes)**
    
    - **API Design:** Specify endpoints, headers, request/response formats
    - **Database Models:** Define queries, table structures, field access patterns
    
    **Phase 4: Comprehensive Analysis (45 minutes)**
    
    - **Security & Risk Analysis:**
        - Authentication & authorization requirements
        - Data protection standards
        - Security test scenarios
        - OWASP Top 10 vulnerability check
    - **Performance & Scalability Analysis:**
        - Database optimization needs
        - Response optimization strategies
        - Scalability planning considerations
    - **Unhappy Paths & Edge Cases:**
        - Authentication failures
        - System failures
        - Input edge cases
        - Error handling strategies
    
    **Phase 5: Implementation Blueprint (30 minutes)**
    
    - **Define Building Blocks:** List new components to create and existing ones to modify
    - **Create Detailed Technical Tasks:** Break down into phased implementation checklist with:
        - Core Infrastructure tasks
        - Business Logic tasks
        - Integration & Routes tasks
        - Testing tasks (Unit, Integration, Security)
        - Documentation & Deployment tasks
        - Time estimates for each phase
    
    **Phase 6: Design Validation (15 minutes)**
    
    - **Acceptance Criteria Coverage:** Verify all requirements addressed
    - **Technical Quality Gates:** Check for over-engineering, security coverage, sprint feasibility
    - **Implementation Readiness:** Confirm all tasks are clearly defined and dependencies available
    
    **Final Output:** Complete GitHub Issue with all design documentation and implementation checklist
    

**Tuesday - Thursday: Implementation Day(s) (The "Engineer Hat")**

1. **Move the Card:** On your board, move the User Story from This Sprint to In Progress.
2. **Daily Stand-up (5-10 mins):** A quick mental check-in: *What did I complete yesterday? What will I do today? Are there any blockers or new learnings that affect my approach?*
3. **💻 Implementation:**
    - Work through the technical task list from Monday's design session
    - Follow the current DoD standards
    - Commit and push frequently, ensuring any CI pipeline remains green
    - Document any deviations from the original design and reasons why
4. **📊 Mid-Sprint Check (Wednesday - 10 mins):**
    - **Progress Assessment:** Am I on track with Monday's task list?
    - **Scope Review:** Has scope crept in? Do I need to adjust?
    - **Blocker Identification:** Any technical challenges requiring design changes?
    - **Quality Check:** Am I maintaining DoD standards?

**Friday: Review & Reflect Day (The "QA & Process Hat")**

1. **Sprint Review (Demo to Yourself):**
    - **✅ Acceptance Criteria Check:** Does the feature do what it's supposed to do from the user's perspective?
    - **🔍 Definition of Done Check:** Was the feature built correctly according to the current DoD?
    - **🔒 Security Validation:** Are security requirements met?
    - **⚡ Performance Check:** Does it meet performance expectations?
    - If all checks pass, close the issue and move the card to Done.
2. **📊 Technical Debt Assessment (15 mins):**
    - **Code Review:** Quick scan for code that needs future refactoring
    - **Documentation:** Are there gaps in documentation?
    - **Testing:** Are there untested edge cases?
    - **Action:** Create technical debt issues for future sprints if needed
3. **🔄 Sprint Retrospective (15 mins):**
    - **🌱 Process Reflection:**
        - What went well this week (in Analysis, Design, Implementation)?
        - What was a bottleneck or challenge?
        - Did the DoD serve me well, or do I need adjustments?
        - What is one small action I can take to improve next week?
    - **📝 Document Learnings:** Update process notes or DoD based on insights

---

### **Phase III: Continuous Refinement**

**Goal:** Maintain momentum, manage technical debt, ensure the project is always ready for the next challenge, and continuously improve quality standards.

**1. Backlog Refinement (The "Look Ahead")**

- **When:** Weekly (e.g., Friday after the Retrospective, or as a dedicated time-block).
- **Action:** Look ahead in your Backlog to stories planned for the next 1-2 sprints.
- **Process:**
    1. **Story Review:** Ensure each story has clear user story format (As a... I want... So that...)
    2. **Acceptance Criteria Creation:** Write specific, testable acceptance criteria using Given-When-Then format
    3. **Story Sizing:** Ensure stories are appropriately sized (can be completed in one sprint)
    4. **Dependency Identification:** Note any dependencies or prerequisites
- **Goal:** Ensure stories are **"Ready for Sprinting"** with complete acceptance criteria
- **Outcome:** Move refined stories from Backlog to Sprint Ready column

**2. Quarterly DoD Evolution Review**

- **When:** End of each Epic or monthly
- **Action:** Comprehensive review of DEFINITION_OF_DONE.md
- **Process:**
    1. **Standards Assessment:** Which DoD items have proven valuable? Which are ignored?
    2. **Technology Maturity:** Have I learned better practices that should be standard?
    3. **Project Phase:** Do quality standards need to increase as the project matures?
    4. **Realistic Calibration:** Remove standards that are unrealistic or not providing value
    5. **New Standards:** Add proven practices that have emerged from recent sprints
- **Outcome:** Updated DoD that reflects current project needs and your skill growth

**3. Architectural Review (The "Architect Hat")**

- **When:** End of major features, or monthly
- **Action:** Re-read and update ARCHITECTURE.md
- **Review Points:**
    - Are architectural decisions still accurate?
    - Do any decisions need revision based on learnings?
    - Are there upcoming refactors needed for technical debt?
    - Do new features require architectural spikes or research?
- **Outcome:** Updated architecture documentation and technical debt backlog

**4. Process Optimization**

- **When:** Monthly or when workflow feels inefficient
- **Action:** Review and refine this workflow document itself
- **Questions:**
    - Are the time allocations realistic?
    - Do any steps consistently get skipped? (Maybe they're not valuable)
    - Are there new practices to incorporate?
    - Is the weekly rhythm sustainable?

---

### **Key Improvements in v4.0:**

- **Streamlined Design Process:** Merged comprehensive sprint design approach into Monday afternoon session
- **Eliminated Redundancy:** Removed duplicate analysis and task planning steps
- **Enhanced Structure:** Clear 6-phase design process with specific time allocations
- **Comprehensive Coverage:** Security, performance, edge cases, and implementation planning in one flow
- **Implementation-Ready Output:** Every Monday produces complete technical blueprint
- **Quality Integration:** DoD evolution and validation built into the rhythm
- **Systematic Documentation:** GitHub issues become complete specifications
- **Added PRD**

This streamlined workflow maintains all the depth and professionalism while eliminating redundant steps between analysis, design, and task planning phases.