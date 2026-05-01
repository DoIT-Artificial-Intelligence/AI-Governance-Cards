# AI Governance Card: AI-Powered Coding Assistants

* Last Revised: 04/10​/26​
* Date Issued: 01/27/2026
* Version: 3.0
* Author: Solomon Abiola, Lauren Maffeo

## Table of Contents
* [Purpose and Scope](#purpose-and-scope)
* [Definition and Autonomy Levels](#definition-and-autonomy-levels)
* [Risk Classification](#risk-classification)
* [Developer Roadmap (Mandatory Do’s and Don’ts)](#developer-roadmap-mandatory-do's-and-don'ts)
* [Risk Analysis and Mitigation](#risk-analysis-and-mitigation)
* [Coding Assistant Tool Status](#coding-assistant-tool-status)
* [Agency Compliance and Intake​](#agency-compliance-and-intake)​
* [Analogy for Understanding](#analogy-for-understanding)

## 1.0 Purpose and Scope

​This governance card forms foundational guidelines for use of AI-powered coding assistants within Maryland’s State government. It builds upon the State’s existing frameworks, including:​

* [Maryland's Responsible AI Policy](https://doit.maryland.gov/policies/ai/Pages/maryland-responsible-ai-policy.aspx)
* [Executive Order Catalyzing the Responsible and Productive Use of Artificial Intelligence in Maryland State Government](https://governor.maryland.gov/Lists/ExecutiveOrders/Attachments/31/EO%2001.01.2024.02%20Catalyzing%20the%20Responsible%20and%20Productive%20Use%20of%20Artificial%20Intelligence%20in%20Maryland%20State%20Government_Accessible.pdf)
* [SB818](https://mgaleg.maryland.gov/2024RS/bills/sb/sb0818E.pdf)

​Maryland’s governance card on AI coding assistants applies to all Executive Branch agencies and all personnel (employees, contractors, and consultants) who develop, maintain, or leverage AI systems to provide services to the State. While agencies must adopt this guidance in its entirety, they can require more stringent guidelines based on their own operational context.​​

## 2.0 Definition and Autonomy Levels
​​AI-powered coding assistants use generative AI to suggest code completions, generate functions, or provide chatbot assistance. While these tools can increase productivity by automating boilerplate tasks, they do not replace developer expertise.

​Developers remain 100% responsible for the final versions of any outputs that AI coding assistants produce. The State correlates risk with the level of autonomy per type of coding assistant:

​​![Coding Assistant Autonomy Levels]()
*This governance card's author created this image using Claude.ai, specifying in their prompt that this image must comply with the Maryland Web Design System (MWDS).​*​

### Low Autonomy (Code Completion): ​​
The tool offers single-line suggestions as the developer types (e.g.​, GitHub Copilot inline). The developer acts as the primary author, and risk is minimal/limited because human review is constant.

### Medium Autono​my (Conversational/Batch):
The tool generates large code blocks based on prompts (e.g., Google AI Studio). The developer acts as a reviewer/editor, and risk is limited, mitigated by the deliberate human action of copying and pasting the code.​​

### High Autonomy (Agentic/Asynchronous):​​
​​The tool can perform sequential steps like editing files and running commands (e.g., Jules, Cline). The developer provides oversight and approval, but risk is high due to the potential for unintended changes or data leakage.

## 3.0 Risk Classification
​​According to the standards in the State of Maryland’s AI risk assessment matrix, AI coding assistants are broadly classified as Limited Risk because they do not autonomously decide critical outcomes for individuals. Human developers and testers are the final decision-makers, because Maryland does not allow AI to make autonomous choices when used for State business.

​​However, the risk tier escalates to High if state staff give​ coding assistants access to sensitive files, ask it to execute commands without explicit approval, or if the tool's privacy settings enable data training. Additionally, Maryland law prohibits using coding assistants from companies based outside of the U.S. (e.g., Mistral, Qwen) due to physical access control requirements.

## 4.0 Developer Roadmap (​Mandatory Do’​s and Don’ts)​​ ​

![AI Coding Assistant Roadmap]​​
*This governance card's author created this image using Claude.ai, specifying in their prompt that this image must comply with the Maryland Web Design System (MWDS).*

### Phase 1: Setup and Configuration​​​
* **Confirm Data:** Level 3 (Confidential) and Level 4 (Restricted) data is not allowed for use in state-provided AI coding assistants.
* **Approved Versions:** Use only versions of coding assistants that do not train on code, data, or other artifacts, such as Enterprise or Government solutions. Individual or free versions that require permitting training and are prohibited​.
* **Privacy Hardening:** You must uncheck "Al​low vendor to u​se code for training" and enable filters that block suggestions matching public code.
* **Limit Access:** Write permissions files (e.g., .gitignore, .copilotignore) to explicitly block the AI from reading sensitive directory segments or environment files containing secrets.

### Phase 2: Responsible Usage​​​
* **Zero Sensitive Data:** Never input PII, PHI, or authentication secrets (API keys, passwords). If code must be generated for a sensitive field, use an abstract placeholder (e.g., USER_SSN).
* **Human-in-the-Loop:** Treat AI as a junior developer: Helpful but potentially flawed. Review every suggestion for correctness, security vulnerabilities (like SQL injection or weak cryptography), and adherence to team style standards.
* **Sanitize Environments:** Use only synthetic data for development and testing.
* **Keep Code Transparent:** Add code comments like // Generated with AI assistance - Tool [date]. Maryland state staff must be able to explain how their code works, regardless of whether they or an AI coding assistant wrote it. Adding code comments confirms your source and provides key metadata.​
* **Assess Impact:** Users must complete an algorithmic impact assessment to confirm no disparate impact on protected groups.

### Phase 3: Final Checks and Commits​​​
* **Validation:** All significant AI-generated code must undergo peer review and rigorous unit/integration testing.
* **Automated Scans:** Run static analysis (linters), SAST, secret scanning, and code quality checks before merging. AI can produce syntactically correct code that passes standard quality checks while harboring subtle logic or runtime vulnerabilities. Mandating this series of scans before deployment, and continuously after, helps mitigate that risk.​​​
* **Accountability:** Before committing, you must fully understand the code and be able to explain how it works: “AI did it" is not an acceptable excuse for bugs or security incidents.
* **Accessibility:** Confirm that AI-generated code meets [WCAG 2.1 AA standards​](https://www.w3.org/TR/WCAG21/) and doesn't introduce usability barriers.

## 5.0 Risk Analysis and Mitigation​​
​
![AI Coding Assistants: Risks and Mitigation Strategies]()
*This governance card's author created this image using Claude.ai, specifying in their prompt that this image must comply with the Maryland Web Design System (MWDS).* ​

​* **Intellectual Property and Copyright:** AI may reproduce licensed code verbatim, raising the risk of copyright infringement or license violations.
    * **Mitigation:** Enable public code filters. If a coding assistant suggests a substantial block of text, manually search public repositories to ensure compliance with open source licenses.
* **Data Leakage:** Cloud-based tools may send proprietary state code as prompts to external services.
    * **Mitigation:** Use FedRAMP-authorized Government clouds where data remains within the U.S. and is not used for model training.
* **Security Vulnerabilities:** AI can suggest outdated algorithms (e.g., MD5) or be manipulated via rules file backdoors to insert malicious instructions.
    * **Mitigation:** Perform dynamic analysis and penetration testing on all output that coding assistants produce.
* **Automation Bias:** Developers may blindly trust AI suggestions due to their sophisticated appearance.
    * **Mitigation:** Maintain healthy skepticism and annotate which code sections were AI-suggested during reviews.
* **Algorithmic Bias:** AI risks embedding discriminatory patterns from training data.
    * **Mitigation:​** Conduct an algorithmic impact assessment to confirm your code ​​has no disparate impact on protected groups.​
* **Transparency Gaps:** No record of AI-generated vs. human code.
    * **Mitigation:** Use inline documentation and log AI tool usage in commit messages.
* **Data Overexposure:** Shares more codebase context with the coding assistant than necessary.
   * **Mitigation:** Use workspace-level ignore files and review tool permissions quarterly.​

## 6.0 Coding Assistant Tool Status

* 🟢 **Approved (Government Versions):**
    * **Claude Code:** Allowed via Maryland's Department of Information Technology (DoIT) using AWS Bedrock. 
    * **​GitHub Copilot:** Allowed via its Enterprise eversion. Requires mandatory opt-out of data training and use of public code filters.
    * **Google AI Studio:** Allowed via paid API keys to ensure it does not train on data. 
    * **Jules:** Allowed if you use a private GitHub repository to prevent data training. [Jules' Privacy Notice](https://jules.google.com/legal) has more details.

To request licenses for the tools above, email doit.intake@maryland.gov and cc your agency's portfolio officer.
​​
* 🟡 **Experimental/Pilot Only:**
    * **Cursor:** Not FedRAMP-authorized. Use only in sandboxes with CIO approval and **Privacy Mode** (Zero Data Retention) enabled.

* 🔴 **Restricted/Not Recommended:**
    * **Cline:** High autonomous risk and lack of managed accountability; not for production use.
    * **Free/Individual Versions:** Prohibited for state business due to data training defaults.

## 7.0 Agency Compliance and Intake
All use of AI coding assistants must be documented in [the State’s AI inventory](https://ai.maryland.gov/ai-inventory) per SB818. Agencies that wish to use unapproved coding assistants must request to use them through [DoIT’s intake process](https://doit.maryland.gov/policies/Departmental/Pages/Intake-Process.aspx).

Once you [submit your intake request](https://doitmaryland.service-now.com/doit?id=sc_cat_item&sys_id=90ebe560db6bd300b302e9ec0b9619e0) to use your coding assistant of choice, you will receive a questionnaire which asks questions about the tool’s **data ownership** (State must retain all rights), **data residency** (U.S.-based only), and **vendor indemnification** for infringing code. Be prepared to answer these questions and explain **why** this coding assistant is the best tool to fulfill your business use case.

Maryland’s AI subject matter experts may reach out during intake to share pre-approved coding assistants that you can use instead. If your proposed coding assistant is still the best fit for your use case, the Software Review Board at Maryland’s Department of Information Technology will assess it for approval to use when conducting State business.

## 8.0 Analogy for Understanding
Using an AI coding assistant is like using an advanced cruise control system. While the system can handle the monotony of the highway (boilerplate code), the driver (the developer) must keep their hands on the wheel and eyes on the road. Their goal is twofold: Arrive at the right destination, and so while keeping everyone else on the road safe from harm.

If the system suggests a dangerous lane change (a security vulnerability) or ignores a Private Property sign (copyright infringement), the driver is the one legally and practically responsible for the outcome. To avoid this, they must follow the right signs (transparent documentation), use only necessary roads (data minimization), and prioritize passenger safety (human-centered design) over their speed of arrival.​​

​The State of Maryland applies this same lens to coding assistants. We pledge to always use AI in service to State residents, employees, and organizations. That involves using AI like coding assistants to deliver state services more effectively. Keeping Maryland’s civil servants in the driver’s seat empowers the State to innovate responsibly. For additional support, explore Maryland’s AI resources and tools at the State’s official​ [​AI website](https://ai.maryland.gov/).
