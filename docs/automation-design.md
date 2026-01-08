# Automation Design – Planned Serverless Workflow

## Purpose
The purpose of this automation layer is to process IT support requests submitted via a cloud-hosted web form, persist ticket data, and notify the IT support team, without requiring any server management.

This automation was intentionally designed but not deployed to maintain zero operational cost while remaining compatible with Azure Free Tier services.

---

## Proposed Architecture Overview
The planned automation uses a serverless, event-driven design based on HTTP triggers.

### Key Components
- Azure Static Web Apps (Frontend)
- Azure Logic Apps (Consumption) or Azure Functions (HTTP-triggered)
- Azure Table Storage
- Email Notification Service (Office 365 / SMTP)
- Azure Monitor

---

## Planned Workflow
1. A user submits an IT support request through the static web frontend.
2. The frontend sends an HTTP POST request containing the ticket details.
3. A serverless backend (Logic App or Azure Function) receives the request.
4. The request payload is validated and parsed.
5. Ticket data is stored in Azure Table Storage with a default status of "Open".
6. An email notification is sent to the IT support team.
7. Execution logs and metrics are captured for monitoring and troubleshooting.

---

## Data Model
Each ticket entity stored in Azure Table Storage includes:
- PartitionKey: `Tickets`
- RowKey: Timestamp-based unique identifier
- Name
- Email
- Issue Description
- Priority
- Status (default: Open)
- CreatedAt timestamp

---

## Security Considerations
- Backend endpoint exposed via HTTPS only.
- Shared secret or API key validation for incoming requests.
- Least-privilege access to Azure Storage using managed identities.
- No secrets stored in frontend source code.

---

## Reliability and Monitoring
- Serverless execution ensures automatic scaling and high availability.
- Azure Monitor planned for execution tracking and failure alerts.
- Retry policies configured for transient failures.

---

## Cost Considerations
The automation layer was evaluated but not deployed to avoid consumption-based costs.

Estimated monthly cost under light usage:
- Logic App (Consumption): <$2
- Azure Functions (Consumption): <$1

The design allows easy activation when cost constraints allow.

---

## Future Enhancements
- Azure AD authentication for ticket submission
- API Management for request throttling and protection
- Infrastructure deployment using Terraform
