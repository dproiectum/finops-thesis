# 1.2 — Current Reporting Process and Observed Difficulties

The existing Power BI Cloud Showback report serves FinOps and some management audiences. The author's professional observations identify four difficulties in producing and distributing the information behind it. They are not a measured assessment of the existing system.

Table 1.1 — Difficulties reported in the current Cloud Showback process.

| Observed difficulty | Consequence for FinOps |
|---|---|
| Changes to sources, cost calculations, KPIs such as savings measures, or visuals require coordination with Data Engineering and Power BI contributors. FinOps has limited direct access to the data platform. | The team cannot inspect or implement every routine change itself. Business rules must be agreed across roles, sometimes through several exchanges; the resulting delay has not been measured. |
| The dashboard is perceived as slow, and some data preparation and calculations take place within Power BI rather than in subject-specific datamarts. | Interactive analysis is less convenient. The respective effects of transformations, the model, queries, visuals, sources and capacity have not been measured. |
| Application owners need access limited to their applications, while domain managers need a view of the applications in their domain. Interactive access at these scopes is not established for all intended recipients. | For some requests, FinOps performs the analysis and sends a selected Excel extract. A new question may require another manual step. |
| Blank values, suspected indicator errors and visual defects have been encountered. | Users may question the result, while the cause may lie in source data, a calculation rule or the visual. The frequency and causes of these incidents have not been measured. |

These difficulties concern the data path, business definitions, visualization and access decisions together. The consultants' locations describe how work is organized, but distance alone has not been shown to cause the handoffs or delay. Nor does the current distribution process imply that Power BI cannot enforce row-level access. Section 7.2 defines how dashboard performance could be diagnosed; Section 1.3 turns the broader reporting problem into the research question.
