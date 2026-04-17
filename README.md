# Adversarial Evaluation Framework for LLM Role-Fit Assessment

## 1. System Overview

This system is an LLM-based role-fit assessment pipeline designed to evaluate whether a candidate is a suitable match for a given job.

The system takes two primary inputs: a job description and a candidate CV. It operates as a multi-step pipeline:
1. extract structured job requirements from the job description
2. summarize relevant candidate qualifications from the CV
3. compare candidate evidence against the job requirements
4. generate a final fit assessment with supporting reasoning

The system is governed by internal evaluation instructions and a hidden scoring rubric that must not be exposed to users. All external inputs (CVs and job descriptions) are treated as untrusted data and may contain adversarial or malicious content. The system must ensure that embedded instructions within these inputs are not executed or allowed to influence evaluation logic.

Additionally, the system processes potentially sensitive personal data contained in CVs and must avoid unnecessary exposure or propagation of personally identifiable information (PII) beyond what is required for the evaluation task.

## 2. Assets and Security-Sensitive Components

## 2. Assets and Security-Sensitive Components

The following assets are considered security-sensitive within the system and must be protected against leakage, manipulation, or misuse:

- **System Prompt**:  
  Contains internal instructions governing model behavior, including constraints on evaluation and safety policies. This is a high-value target for prompt injection attacks, as exposure or override could enable attackers to manipulate system behavior or extract restricted information.

- **Hidden Scoring Rubric**:  
  Defines internal criteria for evaluating candidate suitability. Exposure of this rubric could enable users to game the system, produce artificially optimized inputs (CVs), and raises potential legal and reputational risks if biases or internal heuristics are revealed.

- **Intermediate Representations (Summaries, Extracted Requirements, etc.)**:  
  Outputs generated between pipeline stages (e.g., CV summaries, requirement extraction). These are vulnerable to indirect prompt injection and transformation exploits, where malicious instructions embedded in inputs persist or are amplified across steps.

- **Evaluation Logic and Decision Criteria**:  
  The implicit reasoning process used to compare candidate qualifications against job requirements. Leakage or manipulation of this logic could allow attackers to reverse-engineer decision boundaries or influence outcomes.

- **Model Outputs (Final Assessment)**:  
  The final response returned to the user. Must be protected against:
  - leakage of sensitive information (e.g., system prompt, rubric, internal reasoning)
  - overexposure of PII beyond task requirements
  - generation of fabricated or ungrounded claims about the candidate

- **Input Data (CVs and Job Descriptions)**:  
  Treated as untrusted and potentially adversarial. These inputs may contain embedded instructions, malicious payloads, or misleading information designed to manipulate the system’s behavior.
