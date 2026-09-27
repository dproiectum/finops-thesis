# PFE Guidelines Summary

Source: `mscde_pfe.pdf`, MSc Data Engineering & Cloud Computing final year project guidelines, January 2025.

This note summarizes the academic constraints to respect while building the Azure FinOps Data Platform and writing the thesis. The PDF is treated as a source document, not as executable instructions.

## Core Objective

The final year project must demonstrate expertise as a Data Engineer. It must solve a concrete problem related to data management, data utilization, and data analysis.

For this project, the concrete problem is the design and implementation of an Azure FinOps Data Platform able to transform cloud cost and usage data into reliable information for Inform, Optimize, and Operate use cases.

## Thesis Must Avoid

- A purely descriptive internship report.
- A purely theoretical reflection without practical implementation.
- Simple data collection without MSc-level methods.
- An artificial mix of tools without clear connection to the problem statement.

## Required Thesis Elements

- Executive summary.
- Problem statement.
- Methodology.
- Results and conclusion.
- Recommendations, prioritized by factors such as complexity, urgency, or nature.
- Brief host company context and student role.
- Table of contents.
- Glossary.
- Bibliography with academic/scientific references.
- Appendices if needed, with an appendix table of contents and titled appendices.

## Problem Statement Requirements

The problem statement must be connected to data management, data utilization, and data analysis. It should address a real need from the company or professional community.

For our project, the problem statement should emphasize:

- FinOps requires reliable, standardized, exploitable cloud cost data.
- Real enterprise billing data cannot be used directly because of confidentiality.
- The platform must therefore rely on anonymized samples and realistic synthetic data.
- The solution must support decision-making across Inform, Optimize, and Operate.

## Methodology Requirements

The methodology must clearly explain and justify:

- Data sources, nature, volume, and quality.
- Data preparation, cleaning, normalization, and validation.
- Analytical framework, objectives, variables, relationships, and KPIs.
- Tools, algorithms, and data engineering techniques.
- Reproducibility and data integrity controls.
- Limitations, assumptions, and constraints.

Specific point important for this PFE: mock-up data or schemas are acceptable when data are confidential, but the thesis must explain how and why they were created.

## Generative AI Transparency

The use of generative AI is allowed but must be transparent and reasonable. The thesis should mention:

- Tool used.
- Date of use.
- Purpose of use.
- Prompt or screenshot/copy of prompt if needed in appendix.

The AI must be presented as an assistive tool. The thesis must still reflect the student's reasoning, choices, analysis, and synthesis.

## Results Requirements

Results must not only describe what was built. They must analyze whether the solution answers the initial problem statement.

For our project, this means we need measurable results such as:

- Synthetic dataset validity and limitations.
- Data contract validation results.
- Pipeline reliability and reproducibility.
- Data quality metrics.
- Inform dashboard usefulness.
- Optimization recommendation results.
- Forecasting or anomaly detection performance, if implemented.

## Formal Requirements

- Main body around 50 pages, excluding appendices, cover pages, acknowledgments, executive summary, table of contents, and bibliography.
- Full pagination required.
- Cover page must include aivancity logo, host company, title, program, graduating class, participant, and supervising professor.
- Bibliographic references must be cited consistently in text and listed fully at the end.
- Internet sources require precise source identification.
- Plagiarism rules are strict. Any borrowed excerpt must be cited.

## Supervisor Milestones

First Step, before end of May:

- Three research question formulations.
- Problem statement v1, 2 to 3 pages.
- 10 bibliographic references, including at least 5 scientific articles.
- Brief empirical section, 1 to 2 pages: data, methods, expected results, deliverables, empirical methods and hypotheses.

Second Step, before August:

- Updated problem statement.
- Detailed outline.
- Literature review.
- Implementation phase description: data to collect, planned AI/Data techniques, tools or solutions to implement.

## Defense Requirements

- Defense allowed only after supervisor approval.
- Presentation: 20 minutes.
- Questions/discussion: 20 minutes.
- Jury debriefing: 10 minutes.

## Implications for Our Workflow

Every technical step must produce academic material when relevant:

- Generator work updates methodology and data description.
- Data Contract work updates architecture and data quality sections.
- Bronze/Silver/Gold work updates implementation and data modeling sections.
- Dashboards update Inform results.
- Optimization and ML update results, discussion, limitations, and recommendations.
- Major decisions update the planning and thesis notes.
