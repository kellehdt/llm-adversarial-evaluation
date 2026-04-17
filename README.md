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
