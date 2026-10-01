# 7.5 — Dashboard Access-Control Validation

## 7.5.1 Claim and validation boundary

The dashboard experiment distinguishes authentication from authorization. Authentication establishes who is making a request; authorization determines which business scope that identity may view. The initial PFE experiment uses synthetic personas to test the second property. It cannot establish enterprise authentication, directory accuracy or production readiness. A later IAP test may extend the claim only if the deployed Cloud Run service validates a signed assertion and the retained evidence identifies the tested revision and configuration.

The expected implementation denies access by default. A recognized principal must have an active assignment in `finops_ops.security.user_entitlement`, and that assignment must resolve to an active entry in `business_scope`. The resulting scope must constrain the SQL result set. Removing a navigation item without constraining its underlying query does not satisfy this criterion.

## 7.5.2 Scenario matrix

The same synthetic period and application revision must be used for every scenario. Global totals provide the control population; filtered totals must be smaller than or equal to that population and must reconcile to the authorized applications or projects.

| Scenario | Expected result | Evidence to retain |
|---|---|---|
| FinOps administrator | All dashboard scopes are visible | Persona, visible scope count and global cost total |
| Domain manager | Only applications mapped to the assigned domain are returned | Domain identifier, permitted application list and reconciled cost |
| Subdomain manager | Only the assigned subdomain is returned | Subdomain identifier, application list and reconciled cost |
| Application owner | Only the assigned application is returned | Application code, row count and cost; explicit absence of another application |
| Project manager | Only the assigned project is returned | Project identifier, mapped resources and reconciled cost |
| Principal without entitlement | Access is denied before analytical pages load | Denial screen and application log event without sensitive data |
| Missing identity in IAP mode | Access is denied | HTTP/application outcome and sanitized log event |
| Arbitrary email attempt | No free-text identity control exists | Interface inspection and automated test |

An isolation test is mandatory. For example, an owner entitled to `APP-001` must retrieve the rows and measures assigned to `APP-001` and no row assigned exclusively to `APP-002`. The test must cover every query family used by the dashboard, including resources, subscriptions, owners and exported tabular results if export remains enabled.

## 7.5.3 Demonstration procedure

In demonstration mode, the presenter selects a named persona from a fixed sidebar list. The application displays the resolved role and scope, then refreshes every indicator from constrained queries. A short presentation sequence is sufficient: global FinOps view, domain view, application-owner view and access-denied view. The selector is a test harness over synthetic identities, not an email login form and not a substitute for IAP.

In IAP mode, no persona selector is present. The Cloud Run service must require authentication, and the application must validate the `X-Goog-IAP-JWT-Assertion` value before using the identity. An unsigned email header or user-entered email does not satisfy the authentication requirement.

*Source: Google Cloud, Getting the user's identity and Configure IAP for Cloud Run (accessed 1 October 2026).*

## 7.5.4 Evidence and interpretation

The validation package should contain the executed Git commit, Cloud Run revision, application mode, synthetic period, entitlement rows, automated test output and a small set of screenshots. Screenshots illustrate behavior but do not replace query-level reconciliation. Logs must avoid tokens, assertion contents and unnecessary personal information.

No access-control result is reported in this section before implementation and execution. Passing the persona scenarios would support the limited conclusion that the application applies its configured role and scope rules to the synthetic dataset. Only a separate IAP execution with real authorized test accounts could support a claim about deployed authentication, and neither result would by itself validate the organization's real role hierarchy.
