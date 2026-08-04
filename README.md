# Joblogic (joblogic)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Joblogic is a UK-founded (1998) cloud field service management (FSM) platform for trades, service, and maintenance contractors - covering customers, sites, assets, jobs, engineer scheduling, mobile workforce, quotes, invoices, stock, and PPM (planned preventative maintenance) contracts.

## Access model (read this first)

Joblogic's public API is **not openly self-serve**. Access is customer-provisioned and gated:

- **You must be a Joblogic customer.** API access is provisioned to existing accounts; there is no public sign-up-and-call developer tier.
- **Credentials are issued by Joblogic.** You are given a **Client ID**, **Client Secret**, and **Tenant ID** (a "API Access" self-service app can issue these, and Joblogic Support can too).
- **IP allowlisting behind a firewall.** Joblogic's resource servers sit behind a firewall; your public IP addresses must be allowlisted before requests are accepted. (Live probes of `api.joblogic.com` return `403` from non-allowlisted networks.)
- **UAT first, then production.** Integrations are developed against a per-customer UAT sandbox (web app `https://uat.joblogic.com`, API host `https://uatapi.joblogic.com`, token host `https://uatidentityserver.joblogic.com`) and then promoted.
- **Authentication is OAuth2 client-credentials.** POST `client_id`, `client_secret`, `grant_type=client_credentials`, and your issued `scope` to the IdentityServer `/connect/token` endpoint to get a **Bearer access token that expires after one hour**. Pass it as `Authorization: Bearer <token>` on every request.
- **Multi-tenant.** Most operations require a `tenantId` (GUID) query parameter.
- **Rate limited.** By default up to **100 requests/minute** per client (varies per client, subject to change); over-limit returns **429 Too Many Requests**.

Because the API is IP-allowlisted, the endpoint **paths and methods** in this repo are confirmed from Joblogic's published Postman documentation (`https://apidocs.joblogic.com/`), while request/response **payload schemas** in the OpenAPI and collections are representative and modeled by API Evangelist (they could not be exercised against the live, gated API). See `review.yml` for the confirmed-vs-modeled breakdown.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/joblogic/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/joblogic/refs/heads/main/apis.yml)

## Tags

- Field Service Management
- Job Management
- Scheduling
- Maintenance
- Workforce
- Mobile Workforce
- Trades
- CRM
- SaaS

## Timestamps

- **Created:** 2026-07-12
- **Modified:** 2026-07-12

## APIs

All resource paths sit under `/api/v1`. Production base URL: `https://api.joblogic.com/api/v1` (firewall/IP-allowlisted). UAT base URL: `https://uatapi.joblogic.com/api/v1`.

### Joblogic Customers API

Search, retrieve, create, update, delete, and set the status of customer records - the account entities that own sites, jobs, quotes, and invoices in Joblogic. Includes customer attribute (custom field) management.

- **Human URL:** [https://apidocs.joblogic.com/](https://apidocs.joblogic.com/)
- **Base URL:** `https://api.joblogic.com/api/v1`

#### Tags

- Customers
- CRM
- Field Service Management

#### Properties

- [Documentation](https://apidocs.joblogic.com/)
- [API Reference](https://apidocs.joblogic.com/)
- [OpenAPI](openapi/joblogic-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/joblogic.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/joblogic.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Joblogic Contacts API

Manage contacts attached to customers, sites, suppliers, and subcontractors - create, update, delete, look up contacts by parent entity, and configure the events a contact is notified about.

- **Human URL:** [https://apidocs.joblogic.com/](https://apidocs.joblogic.com/)
- **Base URL:** `https://api.joblogic.com/api/v1`

#### Tags

- Contacts
- CRM
- Notifications

#### Properties

- [Documentation](https://apidocs.joblogic.com/)
- [OpenAPI](openapi/joblogic-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/joblogic.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/joblogic.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Joblogic Sites API

Manage sites - the physical service locations belonging to a customer where assets live and work is carried out. Search, retrieve, create, update, delete, set status, and configure site warnings, plus site attribute management.

- **Human URL:** [https://apidocs.joblogic.com/](https://apidocs.joblogic.com/)
- **Base URL:** `https://api.joblogic.com/api/v1`

#### Tags

- Sites
- Locations
- Maintenance

#### Properties

- [Documentation](https://apidocs.joblogic.com/)
- [OpenAPI](openapi/joblogic-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/joblogic.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/joblogic.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Joblogic Assets API

Manage the equipment and plant assets located at customer sites that Joblogic services and maintains - search, retrieve by integer or unique ID, create, update, and delete assets, with asset attribute (custom field) support.

- **Human URL:** [https://apidocs.joblogic.com/](https://apidocs.joblogic.com/)
- **Base URL:** `https://api.joblogic.com/api/v1`

#### Tags

- Assets
- Equipment
- Maintenance

#### Properties

- [Documentation](https://apidocs.joblogic.com/)
- [OpenAPI](openapi/joblogic-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/joblogic.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/joblogic.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Joblogic Jobs API

The core work-order surface - create, retrieve, search, update, delete, approve, and change the status of jobs, assign contacts, generate job sheets, and record job costs (labour, materials, travel, mileage, overtime, expenses, subcontractor, and schedule-of-rate items).

- **Human URL:** [https://apidocs.joblogic.com/](https://apidocs.joblogic.com/)
- **Base URL:** `https://api.joblogic.com/api/v1`

#### Tags

- Jobs
- Work Orders
- Job Costs

#### Properties

- [Documentation](https://apidocs.joblogic.com/)
- [OpenAPI](openapi/joblogic-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/joblogic.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/joblogic.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Joblogic Visits API

Schedule and manage engineer visits against jobs - search, retrieve, create, update, delete, deploy / re-deploy to a mobile engineer, cancel, and search the scheduler planner.

- **Human URL:** [https://apidocs.joblogic.com/](https://apidocs.joblogic.com/)
- **Base URL:** `https://api.joblogic.com/api/v1`

#### Tags

- Visits
- Scheduling
- Mobile Workforce

#### Properties

- [Documentation](https://apidocs.joblogic.com/)
- [OpenAPI](openapi/joblogic-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/joblogic.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/joblogic.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Joblogic Engineers API

Search and retrieve field engineers, update certificate registration numbers, mark engineers on-call, and run scheduler searches to place visits against the mobile workforce.

- **Human URL:** [https://apidocs.joblogic.com/](https://apidocs.joblogic.com/)
- **Base URL:** `https://api.joblogic.com/api/v1`

#### Tags

- Engineers
- Scheduling
- Workforce

#### Properties

- [Documentation](https://apidocs.joblogic.com/)
- [OpenAPI](openapi/joblogic-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/joblogic.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/joblogic.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Joblogic Quotes API

Create, search, retrieve, update, and delete quotes, read quote costs, assign contacts, approve / reject / revert / cancel a quote, and generate a quote document, with quote attribute (custom field) support.

- **Human URL:** [https://apidocs.joblogic.com/](https://apidocs.joblogic.com/)
- **Base URL:** `https://api.joblogic.com/api/v1`

#### Tags

- Quotes
- Estimates
- Sales

#### Properties

- [Documentation](https://apidocs.joblogic.com/)
- [OpenAPI](openapi/joblogic-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/joblogic.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/joblogic.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Joblogic Invoices API

Create, search, retrieve, update, and delete invoices - including standard, customer-grouped, and PPM invoices - and generate invoice documents. Syncs with accounting integrations such as Xero, QuickBooks, and Sage.

- **Human URL:** [https://apidocs.joblogic.com/](https://apidocs.joblogic.com/)
- **Base URL:** `https://api.joblogic.com/api/v1`

#### Tags

- Invoices
- Billing
- Finance

#### Properties

- [Documentation](https://apidocs.joblogic.com/)
- [OpenAPI](openapi/joblogic-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/joblogic.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/joblogic.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Webhooks

Beyond the REST API, Joblogic can push change events via **outbound webhooks** - an HTTP POST with a JSON payload is sent to a URL you configure when a subscribed event fires (job, visit, invoice, quote, site, asset, and many more, across Created / Updated / Deleted / Status-Updated event types). These are one-way HTTP callbacks, **not** a WebSocket. See `review.yml` for the WebSocket determination (Joblogic does **not** expose a documented public WebSocket API).

## Common Properties

- [Domain Security](security/joblogic-domain-security.yml)
- [Authentication](authentication/joblogic-authentication.yml)
- [LinkedIn](https://www.linkedin.com/company/job-logic)
- [Website](https://www.joblogic.com)
- [Documentation](https://apidocs.joblogic.com/)
- [Plans](plans/joblogic-plans-pricing.yml)
- [Rate Limits](rate-limits/joblogic-rate-limits.yml)
- [Fin Ops](finops/joblogic-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
