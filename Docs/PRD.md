# PRD

### **SALAMATBOT: Product Vision & Strategy Document**

**Owner:** Navid Movafeghi

**Status:** Living Document

**Last Updated:** 6/23/2025

*This document serves as the single source of truth for the strategic direction of SALAMATBOT. It is the North Star that guides our phased development and day-to-day decisions. It defines what we are building, for whom, and why.*

---

### **1. Product Vision**

To become the most trusted and user-friendly digital health companion for Persian speakers, empowering them with reliable, AI-driven medical information and simple, accessible tools to manage their health proactively. We exist to reduce health anxiety, combat misinformation, and promote well-being through technology.

---

### **2. Target Audience**

We are building for people who actively seek to manage their health or the health of their loved ones. While our tool is open to all, our design and feature decisions will prioritize the following primary personas:

- **Primary Persona 1: The "Worried Well" (Sara, 32)**
    - **Profile:** A tech-savvy individual who gets anxious about health symptoms and frequently uses web searches for answers.
    - **Pain Point:** Overwhelmed by conflicting, unreliable, and often frightening information online.
    - **What she needs from us:** Quick, trustworthy, and calming answers to her general health questions to help her decide if she needs to see a doctor.
- **Primary Persona 2: The Caregiver (Reza, 45)**
    - **Profile:** Manages the health of his aging parents, including their medications and multiple doctor's appointments.
    - **Pain Point:** Juggling complex schedules and health information for others is stressful and disorganized.
    - **What he needs from us:** A simple, consolidated tool to look up drug interactions (Phase 1) and manage schedules (Phase 3).

---

### **3. Business Model**

SALAMATBOT operates on a **Freemium Subscription** model.

- **Free Trial:** All new users receive a **10-question free trial** to experience the full value and accuracy of the core chatbot.
- **Paid Subscription:** To ask more than 10 questions and gain access to all current and future features (such as the Health Management Suite), users must subscribe to a simple, low-cost monthly plan.
- **Philosophy:** This model provides a risk-free way for users to validate our service's trustworthiness while generating the sustainable revenue needed for continued development, research, and operation.

---

### **4. High-Level Phased Roadmap**

Our development is structured into strategic phases. Each phase has a clear goal and builds upon the success of the last.

**Phase 1: Utility & Safety Validation**

- **Goal:** To answer one critical question: **Will Persian speakers find an AI-powered medical chatbot useful, safe, and trustworthy enough for repeat use?**
- **Logic (De-Risking Principle):** This phase isolates our most fundamental assumption. Before we build a business, we must prove we have a product that people trust and value. We will launch a completely free version with no account or payment friction to maximize adoption and gather the purest data on utility.
- **Key Features:**
    - A public, anonymous conversational AI chat interface.
    - Prominent disclaimers on every response.
    - Simple "👍 / 👎" feedback buttons on each answer.
    - An optional link for users to provide qualitative text feedback.
- **Decision Gate (Success Metrics):** We will not proceed to Phase 2 until we achieve the following:
    - **Core Engagement:** 2,500+ total questions asked.
    - **Answer Quality:** >70% "Helpful" (👍) rating from user feedback.
    - **User Trust:** >10% rate of returning visitors.
    - **Qualitative Insight:** 20+ pieces of written feedback to inform the next phase.

**Phase 2: Business Model Validation (Monetization)**

- **Goal:** To validate our business model hypothesis: **Will the engaged users from Phase 1 convert into paying subscribers?**
- **Logic (Value-First Principle):** Having proven the utility of the core product, we now test if the value is high enough to support a sustainable business. This introduces the necessary infrastructure for a commercial product.
- **Key Features:**
    - **Secure User Accounts (Principle 4):** Email/password registration and login.
    - **Freemium Logic:** Implement the 10-question free trial for all new registered users.
    - **Subscription & Payment Gateway (Principle 4):** A seamless flow for users to subscribe to a monthly plan.
- **Primary Success Metrics for This Phase:**
    - **Free-to-Paid Conversion Rate.**
    - **Monthly Recurring Revenue (MRR).**

**Phase 3: Engagement & Retention (The Health Management Suite)**

- **Goal:** To increase user retention and product "stickiness," evolving SALAMATBOT from a transactional tool into a long-term health companion.
- **Logic ("No Half-Features" Principle):** Now that we have a validated product and a working business model, we invest in features that solve deeper user problems (for Sara and Reza) and create long-term value, reducing churn.
- **Key Features:**
    - **Proactive Health Management (Principle 2):** Medication Reminders, Appointment Reminders.
    - **Consolidated Personal Health Record (Principle 3):** A simple journal for users to log key metrics (e.g., blood pressure, blood glucose).
- **Primary Success Metrics for This Phase:**
    - **Month-over-Month User Retention.**
    - **Adoption Rate** of new health management features.

---

### **5. Overarching Success Metrics**

These are the key performance indicators (KPIs) that measure the overall health and success of the SALAMATBOT product, across all phases.

- **Growth & Adoption:**
    - **Monthly Active Users (MAU):** The total number of unique users who engage with the product each month.
    - **New Subscribers per Month:** The rate at which we are growing our paying user base.
- **Engagement & Value:**
    - **Free-to-Paid Conversion Rate:** The percentage of free trial users who become paying subscribers. This is the primary indicator of our business model's health.
    - **User Retention (Month-over-Month):** The percentage of users who remain subscribed. This indicates long-term value.
- **Financial:**
    - **Monthly Recurring Revenue (MRR):** The total predictable revenue generated from subscriptions each month. This is the ultimate measure of a sustainable business.

### **6. Core Functional Principles (The "What We Do")**

*This section outlines the fundamental capabilities that define the product's value proposition. All major features will align with these core principles.*

- **Principle 1: Conversational Medical Inquiry:** The core of the product is an AI-powered chat interface where users can ask general medical questions in natural Persian and receive safe, reliable, and context-aware answers.
- **Principle 2: Proactive Health Management:** The product will provide tools that help users actively manage their health, such as setting reminders for medications and appointments. This functionality moves the user from a reactive to a proactive state.
- **Principle 3: Consolidated Personal Health Record:** Users must have a secure, private place to record and track their key health metrics over time (e.g., blood pressure, blood glucose).
- **Principle 4: Secure Account & Subscription Management:** The product will provide robust functionality for users to manage their accounts, privacy settings, and subscription status seamlessly.

---

### **7. Core Non-Functional Requirements (NFRs) (The "How Well We Do It")**

*This section defines the quality attributes and technical standards our product must meet. These are not features, but promises about the system's performance, reliability, and security. They are the definition of "quality" for SALAMATBOT.*

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