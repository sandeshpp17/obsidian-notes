## 🧩 1. Multi-Tenancy and Group Isolation

**Goal:** Validate that each tenant (group) operates independently without data or visibility leakage.

| Test Case                                                                    | Expected Result                                                    | Validation Method                                                    |
| ---------------------------------------------------------------------------- | ------------------------------------------------------------------ | -------------------------------------------------------------------- |
| Create multiple top-level groups (e.g., Tenant-A, Tenant-B).                 | Each group is created successfully with isolated visibility.       | Login with different users and verify visibility of projects/groups. |
| Create subgroups and projects under each tenant.                             | Subgroups and projects inherit correct visibility and permissions. | Inspect project access levels in **Settings → Members**.             |
| Add users to Tenant-A and Tenant-B with different roles (Owner, Developer).  | Users should see and access only their assigned groups.            | Cross-check via impersonation or separate logins.                    |
| Attempt cross-tenant access (e.g., Tenant-A user to view Tenant-B projects). | Access should be denied or hidden entirely.                        | Confirm via UI/API (404 or unauthorized response).                   |

✅ _Pass Criteria:_  
No user from one group can view, list, or interact with resources from another group or project.

---

## ⚙️ 2. Project Setup, CI/CD Pipeline, and Runner Functionality

**Goal:** Ensure each tenant can host its own repositories and pipelines independently.

| Test Case                                                    | Expected Result                                            | Validation Method                           |
| ------------------------------------------------------------ | ---------------------------------------------------------- | ------------------------------------------- |
| Push sample source code to a project repository.             | Code is pushed successfully and visible in GitLab UI.      | Git push / GitLab UI verification.          |
| Create `.gitlab-ci.yml` with basic build/test/deploy stages. | Pipeline triggers automatically on commit.                 | Observe CI/CD → Pipelines page.             |
| Register a runner for Tenant-A at group or project level.    | Runner appears only in Tenant-A and can execute jobs.      | **Settings → CI/CD → Runners** in Tenant-A. |
| Execute a pipeline using the registered runner.              | Job runs successfully and completes all stages.            | Job log shows correct execution steps.      |
| Register another runner for Tenant-B.                        | Tenant-B’s runner is isolated and not visible in Tenant-A. | Cross-check visibility via UI or API.       |

✅ _Pass Criteria:_  
Pipelines run successfully per tenant using isolated runners, with no shared visibility across groups.

---

## 🧱 3. Runner Isolation and Resource Governance

**Goal:** Validate runner isolation and prevent unauthorized cross-group access.

| Test Case                                            | Expected Result                                                      | Validation Method                                             |
| ---------------------------------------------------- | -------------------------------------------------------------------- | ------------------------------------------------------------- |
| Assign group-level runners to Tenant-A and Tenant-B. | Each runner executes only jobs from its assigned group.              | Run pipelines in both groups and confirm correct runner used. |
| Verify shared runners (if enabled).                  | Shared runners respect isolation policy or are disabled for tenants. | Admin → Runners overview.                                     |
| Check system resource utilization.                   | Runners operate within resource quotas.                              | Monitor Kubernetes / VM metrics.                              |

✅ _Pass Criteria:_  
No runner should process jobs from unassigned tenants; shared runners must be explicitly controlled.

---

## 📦 4. Central Container Repository (Harbor / GitLab Registry)

**Goal:** Validate central image management and tenant-based access control.

| Test Case                                                         | Expected Result                                          | Validation Method                            |
| ----------------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------- |
| Build and push Docker image from CI pipeline to central registry. | Image successfully pushed to repository.                 | Check registry dashboard (Harbor or GitLab). |
| Verify image visibility and pull access.                          | Images are visible only to the owning project or tenant. | Attempt cross-tenant pulls → access denied.  |
| Configure image pull in another environment using CI/CD token.    | Pull succeeds with valid credentials only.               | Inspect logs and authentication results.     |

✅ _Pass Criteria:_  
Central container registry supports project-scoped repositories with strict access control and isolated image namespaces.

