# Azure Cloud IT Help Desk (Cost-Constrained Design Project)

This project demonstrates the design and partial implementation of a cloud-based IT help desk system using Microsoft Azure. The focus is on cloud architecture, serverless design principles, identity awareness, and cost-conscious decision making.

The solution is intentionally scoped to remain within Azure free-tier limits while clearly documenting how it would be productionized in a real enterprise environment.

---

## Problem Statement

Small IT teams often need a simple, cloud-based way to collect and manage support requests without maintaining servers or incurring unnecessary infrastructure costs.

This project explores how such a system can be designed using Azure-native services with an emphasis on scalability, security, and operational simplicity.

---

## Live Demo

The static frontend for this project is publicly accessible and hosted using **Azure Static Web Apps**.

🔗 **Live Demo URL:**  
https://zealous-island-063f0861e.6.azurestaticapps.net

The demo showcases an HTML-based IT support request form and demonstrates GitHub-integrated CI/CD deployment to Azure.

> Note: Backend automation is intentionally not enabled to maintain zero operational cost.

---

## Current Implementation (Deployed)

The following components are fully deployed and operational:

- **Azure Static Web Apps**
  - Hosts a static HTML-based IT support request form
  - Integrated with GitHub for continuous deployment
- **GitHub Repository**
  - Source control and project documentation
- **Azure Storage Account**
  - Planned persistence layer using Table Storage (schema defined)

### Current Architecture
![Current Architecture](architecture/current-architecture.png)

This implementation represents the minimum viable cloud footprint while remaining within zero-cost constraints.

---

## Planned Automation Architecture (Design-Only)

To enable full ticket automation, a serverless backend was designed but not deployed due to cost considerations.

### Planned Components

- **Serverless Backend**
  - Azure Logic Apps (Consumption) or Azure Functions (HTTP-triggered)
- **Azure Table Storage**
  - Ticket persistence with default status set to `Open`
- **Email Notifications**
  - Automatic alerts to IT support staff
- **Azure Monitor**
  - Logging, metrics, and alerting

### Planned Architecture
![Planned Architecture](architecture/planned-architecture.png)

### Planned Workflow

1. User submits an IT support request via the static web form
2. Form data is sent via HTTPS (HTTP POST) to a serverless backend
3. Ticket data is validated and stored in Azure Table Storage
4. An email notification is sent to the IT support team
5. Execution logs and metrics are captured using Azure Monitor

---

## Data Model (Planned)

Each ticket stored in Azure Table Storage would include:

- PartitionKey: `Tickets`
- RowKey: Timestamp-based unique identifier
- Name
- Email
- Issue Description
- Priority
- Status (`Open` by default)
- CreatedAt timestamp

---

## Security & Identity Considerations

- HTTPS-only endpoints
- Least-privilege access to Azure Storage
- Planned use of managed identities
- No secrets stored in frontend source code
- Clear separation of frontend and backend responsibilities

---

## Cost Optimization Decisions

This project prioritizes cost awareness and efficient cloud usage:

- All deployed resources remain within Azure Free Tier limits
- Consumption-based automation services were evaluated but not activated
- Architecture allows backend automation to be enabled later with minimal changes

---

## Future Enhancements

- Enable serverless automation (Logic Apps or Azure Functions)
- Azure AD authentication for ticket submission
- Infrastructure as Code (Terraform)
- API Management for request validation and throttling
- Metrics dashboard and reporting
