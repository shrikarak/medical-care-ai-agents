# AI-Powered Multi-Agent System for Patient Journey Management

**Copyright (c) 2026 Shrikara Kaudambady. All rights reserved.**

## 1. Introduction

Navigating the healthcare system can be a complex and fragmented process for patients. From initial symptom assessment to booking an appointment and verifying insurance, the journey involves multiple steps and administrative hurdles. This complexity can lead to delays in care and a poor patient experience.

This project provides a Jupyter Notebook that simulates an advanced **multi-agent AI system** designed to automate and manage this entire patient journey. It features a team of specialized AI agents that collaborate to handle a patient case from initial contact to final resolution, demonstrating how AI can serve as a powerful "digital front door" for healthcare providers.

## 2. The Solution Explained: A Collaborative AI Team

This solution is modeled as a "team of experts" where a central coordinating agent delegates tasks to specialists. This modular architecture is robust, scalable, and easy to understand.

### 2.1. The Simulated Environment
To create a self-contained demonstration, we simulate the core IT systems of a healthcare provider:
*   **`PatientDB`:** A mock database of Electronic Health Records (EHR), containing patient history, allergies, and insurance information.
*   **`DoctorCalendar`:** A mock scheduling system with available and booked appointment slots.

### 2.2. The Specialist Agents
Each specialist agent is a Python class with a narrowly defined role and a set of "tools" (methods) to perform its function.
*   **`TriageAgent`:** Acts as the first point of contact. Its `classify_urgency` tool performs a keyword-based analysis of the patient's reported symptoms to categorize the case as `Emergency`, `Urgent`, or `Non-Urgent`.
*   **`MedicalHistoryAgent`:** Functions as an automated medical archivist. Its `get_summary` tool queries the `PatientDB` to retrieve a concise summary of the patient's relevant history and allergies.
*   **`InsuranceAgent`:** Handles the administrative checks. Its `verify_coverage` tool checks the `PatientDB` to confirm if the patient's insurance plan is active.
*   **`SchedulerAgent`:** Manages appointment logistics. Its `schedule_appointment` tool finds the next available slot in the `DoctorCalendar` and books it.

### 2.3. The `CareCoordinatorAgent` (The Orchestrator)
This is the master agent that embodies the core logic of the patient journey. It does not perform the tasks itself but intelligently orchestrates the specialist agents in a specific sequence:
1.  **Triage:** It first calls the `TriageAgent`. If the case is an emergency, the process stops, and an appropriate recommendation is made.
2.  **Information Gathering:** For non-emergencies, it calls the `MedicalHistoryAgent` to get context.
3.  **Verification:** It then calls the `InsuranceAgent` to clear the administrative hurdle. If insurance is inactive, the process is halted, and a different recommendation is issued.
4.  **Action:** Once all checks are passed, it calls the `SchedulerAgent` to book an appointment.
5.  **Reporting:** Finally, it compiles all the findings from the other agents into a comprehensive summary report of the completed patient journey.

## 3. How to Use the Notebook

### 3.1. Prerequisites

This project is self-contained and uses only standard Python libraries. No special installation is required beyond a working Jupyter environment.

### 3.2. Running the Notebook

1.  Clone this repository:
    ```bash
    git clone https://github.com/shrikarak/medical-care-ai-agents.git
    cd medical-care-ai-agents
    ```
2.  Start the Jupyter server:
    ```bash
    jupyter notebook
    ```
3.  Open `patient_journey_simulation.ipynb` and run all cells. The notebook will simulate several different patient scenarios (a routine case, an emergency, and an insurance failure) and print the detailed, step-by-step log of the agents' collaboration for each one.

## 4. Real-World Deployment and Vision

This simulation is a powerful blueprint for a production-level healthcare automation platform.

1.  **Integrating with Real Systems:** The key to deployment is replacing the mock environment classes with real API calls.
    *   The `MedicalHistoryAgent` would query a real EHR system via the **HL7/FHIR** standard.
    *   The `InsuranceAgent` would connect to a **healthcare clearinghouse API** for real-time eligibility checks.
    *   The `SchedulerAgent` would interact with a real clinical scheduling system's API (e.g., Epic, Cerner, or a standalone service).

2.  **Upgrading Agent Intelligence:**
    *   The `TriageAgent`'s simple keyword logic would be replaced with a sophisticated **NLP classification model** (e.g., a fine-tuned BERT or T5 model) trained on real medical triage notes.
    *   The `CareCoordinatorAgent`'s `if/then` logic could be upgraded to a **Large Language Model (LLM)**. An LLM could handle much more complex and ambiguous patient journeys, dynamically re-ordering steps and making more nuanced decisions based on the combined outputs of the specialist agents.

This multi-agent architecture provides a scalable and maintainable way to build powerful AI systems that can automate complex, real-world workflows.
