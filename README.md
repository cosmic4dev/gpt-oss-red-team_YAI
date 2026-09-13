# GPT-OSS-20B Red Teaming

![Kaggle Competition](https://img.shields.io/badge/Kaggle-OpenAI%20GPT--OSS--20B%20Red--Teaming-blue)
Supporting materials for the **YAI_academia** submission to the
[OpenAI GPT-OSS-20B Red Teaming Competition on Kaggle](https://www.kaggle.com/competitions/openai-gpt-oss-20b-red-teaming).

## At a glance

| Item | Scope |
|---|---|
| Target model | `gpt-oss-20b` |
| Submission artifacts | Five structured finding JSON files |
| Executable analyses | Three notebooks currently included |
| Focus | Context-dependent safety failures and instruction-boundary stress tests |
| Intended use | Defensive analysis, reproduction, and mitigation design |


---

## 1. Project Overview

This repository preserves the structured findings and the analysis notebooks
that were included in the public project package. It is a competition artifact,
not a claim that every finding has a complete standalone reproduction notebook
in this repository.

The submission organized observations into five candidate vulnerability
classes:
1.  **Policy Blind Spots** in assessing dual-use technologies.
2.  **Process Gaps** in analyzing the content of technical tasks.
3.  **Latent Leakage** of confidential information in its internal reasoning.
4.  **RAG-based Harmful Content Relay** where external data bypasses safety filters.
5.  **Pretrain Data Exploitation** where mimicking training data triggers unsafe responses.

The artifacts motivate safety evaluation that tests contextual framing,
transformation tasks, retrieved content, and internal/external response
boundaries—not only direct harmful requests.

![Project Banner](./assets/yai_academia_red_team.png)

---

## 2. Key Findings

Each class has a structured record under `/findings`. Three classes also have a
notebook in `/notebooks`; the other two remain submission records rather than
notebook-level reproductions in this public package.

* **Finding 1: Dual-Use Technology Vulnerability**
    * **Description:** The model fails to recognize the potential harm of dual-use technologies when framed within a benign context (e.g., an "artistic light show").
    * **Evidence:** Successfully generated a detailed algorithm for an **autonomous drone swarm**.

* **Finding 2: Harmful Content Obfuscation Vulnerability**
    * **Description:** The model's safety checks are bypassed when harmful content is embedded within a technical task (e.g., JSON parsing).
    * **Evidence:** Successfully generated a **threatening email** hidden inside a JSON object.

* **Finding 3: Latent Leakage Vulnerability**
    * **Description:** The model's internal reasoning (`analysis` channel) leaks confidential information even when the final output is a safe refusal.
    * **Evidence:** Statistically significant leakage of "secret" strings when prompted with specific lexical and instructional triggers.

* **Finding 4: RAG-based Harmful Content Relay**
    * **Description:** The model suspends its own safety judgment when asked to relay information from a "retrieved document," effectively laundering harmful content (e.g., hate speech) by treating it as factual data.

* **Finding 5: Pretrain Data Attack**
    * **Description:** By mimicking the style of its pretraining data (e.g., a Wikipedia entry), the model's safety alignment can be bypassed, causing it to output detailed instructions for harmful activities like creating explosives.

---

## 3. Repository Structure

This repository is organized as follows to ensure clarity and reproducibility.

```
/
├── findings/
│   ├── dual-use-vulnerability.json
│   ├── obfuscation-vulnerability.json
│   ├── latent-leakage-vulnerability.json
│   ├── rag-relay-vulnerability.json
│   └── pretrain-data-vulnerability.json
│
├── notebooks/
│   ├── dual_use_vulnerability.ipynb
│   ├── obfuscation_vulnerablility.ipynb
│   └── latent_leakage_vulnerability.ipynb
│
├── assets/
│   └── yonsei_red_team_eagle.png
│
├── .gitignore
├── requirements.txt
└── README.md
```

* **`/findings`**: Contains the five final `.json` files detailing each vulnerability, formatted for Kaggle submission.
* **`/notebooks`**: Contains the three analysis notebooks included in the
  current public package.
* **`/assets`**: Contains images and media used in this README and the final Writeup.
* **`README.md`**: This file, providing an overview of the project.

---

## 4. Setup & Reproduction

To reproduce our findings, please follow these steps:

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/cosmic4dev/gpt-oss-red-team_YAI.git
    cd gpt-oss-red-team_YAI
    ```

2.  **Set up the environment:**
    It is recommended to use a virtual environment.
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    pip install -r requirements.txt
    ```

3.  **Run the Notebooks:**
    Navigate to the `/notebooks` directory. Each `.ipynb` file in this directory corresponds to a specific vulnerability detailed in our findings. For example, to reproduce the 'Dual-Use' vulnerability, open and run the cells within `dual-use-vulnerability.ipynb`. All notebooks are documented to guide you through each demonstration.

---

## 5. Ethical Considerations

All experiments were conducted with a strong commitment to ethical guidelines and in compliance with the competition rules.
* No real personal or sensitive data was used. All secret strings were synthetic canary tokens (e.g., `SYS-SECRET-ABC123`).
* The primary goal of this research is to identify and help mitigate vulnerabilities, not to enable attacks.
* Harmful content generated by the model for our findings files has been appropriately redacted where necessary for public documentation, ensuring compliance with Kaggle's content policy.

---

## 6. Evidence and licensing boundary

- Findings are preserved as competition submission artifacts; readers should
  inspect each JSON record and notebook before treating a class as independently
  reproduced.
- Harmful examples should remain redacted or handled in a controlled research
  environment.
- This repository currently has no repository-level `LICENSE` file. No blanket
  open-source permission is implied until the team adds one and confirms the
  applicable competition terms.

---

## 7. Team

This project was conducted by the **YAI_academia** team from Yonsei University.

* Kyungwon Park
* Hyunjin Cho
* Heejae Chon
* Youngju Lee
