# Project Roadmap and Open-Source Module Plan

Goal
Build an integrated open-source UK property management and maintenance platform that can run in production and help a management company manage properties, tenants, rent, maintenance, compliance, contractors, and reporting.

Core strategy
- Use a modular platform design
- Prefer open-source tools for each domain
- Use Odoo Community as the main ERP foundation if a full integrated business layer is needed
- Add custom workflows and a web portal to handle unique UK property operations
- Add an AI agent that can continuously scan for more suitable open-source apps and tools

1. Business domains to cover

A. Property portfolio
- property records
- units and blocks
- landlords and owners
- addresses and maps
- property status and occupancy
- valuation and condition tracking

B. Lettings and tenancy
- tenants and guarantors
- tenancy agreements
- application workflow
- rent schedule
- notice periods
- renewals
- lease expiry alerts
- arrears tracking

C. Rent and finance
- rent schedules
- payment collection
- arrears dashboards
- landlord statements
- expenses and service charges
- invoice generation

D. Maintenance and repairs
- work orders
- maintenance requests
- priorities and SLAs
- inspection workflows
- contractor assignments
- asset lifecycle tracking
- cost tracking

E. Compliance and safety
- gas safety
- EICR
- PAT testing
- fire checks
- Legionella
- asbestos
- HMO licensing
- health and safety inspections
- expiry reminders and escalation

F. Contractors and suppliers
- contractor profiles
- rates and contracts
- insurance checks
- job histories
- procurement and approvals

G. Documents and compliance archive
- tenancy docs
- certificates
- inspection reports
- invoices
- notices
- legal documents

H. Reporting and dashboards
- occupancy rate
- arrears summary
- maintenance backlog
- compliance due dates
- landlord KPIs
- agent productivity

2. Recommended open-source modules and tools

Core platform
- Odoo Community
  - best open-source integrated ERP foundation
  - covers CRM, sales, accounting, inventory, project, HR, helpdesk, assets, documents
  - useful for property operations and business workflows

Database and data model
- PostgreSQL
  - primary database
- TimescaleDB (optional)
  - useful for maintenance events, telemetry, and time-series reporting

Backend and API
- FastAPI
  - modern API framework
  - suitable for custom property and maintenance services
- Django Rest Framework (alternative)
  - good if the team prefers Django

Frontend
- Next.js
  - modern web dashboards for agents and staff
- React + TypeScript
  - reusable UI components
- OpenAPI-generated clients
  - strongly typed API integration

Authentication and access control
- Keycloak
  - SSO and user management
- Authentik
  - alternative for self-hosted identity management

Workflow and automation
- n8n
  - automates approvals, notifications, and syncing with external tools
- Celery or RQ
  - background jobs for scheduled reminders, reports, and processing

Document and file management
- MinIO
  - S3-compatible object storage
- Nextcloud or Paperless-ngx
  - document management and OCR if needed

Search and reporting
- Elasticsearch
  - search and analytics
- Metabase
  - dashboards and reporting
- Apache Superset
  - alternative BI dashboard tool

AI agent
- LangChain or LlamaIndex
  - orchestration for the AI agent
- OpenAI API or local open-source LLM
  - OpenAI for production simplicity
  - Llama 3 / Mistral / Qwen for local privacy-first deployments
- Qdrant or pgvector
  - vector storage for repository and document matching
- n8n + AI agent integration
  - task orchestration and event-driven workflows

Observability and deployment
- Docker
  - containerized services
- Docker Compose or Kubernetes
  - local deploy or prod deploy
- Prometheus + Grafana
  - system metrics and monitoring
- GitHub Actions
  - CI/CD automation

3. Recommended product architecture

Recommended architecture for this project
- Frontend: Next.js dashboard for management team, tenants, and contractors
- Backend API: FastAPI
- Business ERP layer: Odoo Community
- Database: PostgreSQL
- Task queue: Celery
- Document storage: MinIO
- AI agent: Python service with LangChain + vector DB + LLM
- Automation: n8n

High-level system modules
- Property module
- Lease module
- Rent module
- Maintenance module
- Compliance module
- Contractor module
- Document module
- Reporting module
- AI recommendation engine

4. Core module feature list

Property module
- add/update property details
- assign property manager
- attach units and blocks
- define occupancy and status
- property documents and photos

Tenant and lease module
- tenant profiles
- guarantor records
- tenancy schedule
- rent amount and due dates
- renewals and notice reminders
- communication history

Rent and accounts module
- rent collection
- book keeping integration
- arrears summary
- payment status
- landlord statements

Maintenance module
- raise a maintenance request
- assign contractor
- log material costs
- schedule repair windows
- track completion and SLA
- link assets and properties

Compliance module
- track required certificates
- set renewal alerts
- attach inspection records
- link to property and asset
- generate missing-compliance dashboard

Contractor module
- contractor directory
- approved vendors
- insurance validation
- contractor reviews and jobs
- timesheets and costs

Document module
- upload tenancy docs and certificates
- store inspection reports and legal notices
- search by property, tenant, or date
- permission-based access

AI agent module
- compare open-source property tools, maintenance tools, and compliance software
- rank by license, features, UK readiness, and deployment requirements
- search GitHub and web sources for updated apps
- create shortlist with pros, cons, and fit score
- generate recommendation report for the business

5. AI agent design

AI agent purpose
The AI component should help the management company find the best apps and modules faster.

Agent tasks
- search GitHub for relevant repositories
- search web sources for property management and compliance tools
- evaluate open-source licenses
- identify if a tool supports UK property workflows
- compare features such as rent, maintenance, compliance, and tenant management
- rate solutions based on business fit
- suggest internal modules to build if the open-source options are incomplete

Agent inputs
- target business type: residential leasing, property management, maintenance, mixed-use portfolio
- geography: UK
- requirements: compliance, letting, rent collection, contractors
- constraints: open-source only, self-hosted preferred, low-cost

Agent outputs
- ranked shortlist of tools
- recommended stack
- “build vs buy” decision
- integration notes
- issue list and module gaps

Recommended AI stack
- Python service with LangChain
- vector DB: Qdrant or pgvector
- model: local LLM or OpenAI API
- fallback: rule-based comparison engine

6. MVP plan

Phase 1 – Foundation
- setup repo and environment
- PostgreSQL and Docker Compose
- FastAPI backend
- Next.js frontend
- auth layer
- property CRUD

Phase 2 – Lettings and rent
- tenants
- lease records
- rent schedules
- payment status
- arrears alerts

Phase 3 – Maintenance and compliance
- maintenance tickets
- contractors
- inspections
- compliance reminders
- certificate expiry tracking

Phase 4 – Reporting and documents
- landlord statements
- dashboards
- document storage
- file uploads and search

Phase 5 – AI agent
- GitHub and web research agent
- scoring framework
- shortlist generation
- recommendations and reports

Phase 6 – Production readiness
- backup and restore
- monitoring
- audit logs
- permissions and RBAC
- deployment pipeline

7. Minimum viable data model

Entities
- User
- Role
- Company
- Portfolio
- Property
- Unit
- Tenant
- Guarantor
- Lease
- RentSchedule
- Payment
- MaintenanceRequest
- Contractor
- ServiceOrder
- ComplianceCheck
- Certificate
- Document
- Inspection
- Task
- Alert
- Report

Key relationships
- Company has many portfolios
- Portfolio has many properties
- Property has many units
- Lease belongs to property and tenant
- RentSchedule belongs to lease
- MaintenanceRequest belongs to property and tenant
- ComplianceCheck belongs to property and asset
- Contractor has many service orders
- Document can belong to property, tenant, lease, or compliance item

8. Recommended deployment model

Local development
- Docker Compose
- PostgreSQL
- Redis
- backend
- frontend
- n8n
- MinIO
- vector DB
- AI agent service

Production deployment
- self-hosted on VPS or cloud VM
- Kubernetes for scaling if needed
- backup strategy with Postgres dumps and object storage backup

9. Build recommendation

Best realistic path
- Start with a modular backend and dashboard
- Add one domain at a time: property, then lettings, then maintenance, then compliance
- Integrate AI after the core structure is stable
- Build the AI layer as an internal decision engine, not as a core operational dependency at first

Open-source stack recommendation
- Backend: FastAPI
- Frontend: Next.js
- Database: PostgreSQL
- Identity: Keycloak
- Storage: MinIO
- Automation: n8n
- AI: LangChain + Qdrant + local/open LLM
- ERP: Odoo Community as optional integration layer

10. Recommended roadmap for this repo

Now
- define business domain and user roles
- create data models
- implement property and tenant CRUD
- add maintenance and compliance entities

Next
- add rent and accounting flows
- build dashboards
- add notifications
- add document upload and search

Later
- add AI agent service
- create app comparison engine
- build recommendation scoring
- add export and reporting

11. Final practical recommendation
The system should not be built as one giant app from day one. It should be built as a modular platform where each domain is independent but connected.

The strongest strategy is:
- Odoo Community as the ERP backbone if you want maximum integration
- FastAPI + Next.js custom app for user workflows and dashboards
- AI agent for researching better tools and modules
- Open-source modules for maintenance, compliance, documents, and reporting

This gives you a platform that can actually run and evolve without locking you into a closed ecosystem.

12. Suggested first deliverables for this repo
- property model
- tenant and lease model
- maintenance request model
- compliance check model
- contractor model
- AI agent scaffold
- dashboard skeleton
- Docker Compose starter
- README with setup instructions

This is the foundation that can become a real management company platform.
