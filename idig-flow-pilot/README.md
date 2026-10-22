<img src="https://upload.wikimedia.org/wikipedia/commons/5/51/IBM_logo.svg" alt="IBM Logo" width="100" />

# IBM API Connect Flow Pilot

**Skills and MCP servers for IBM API Connect Flow Pilot**

[![agentskills.io](https://img.shields.io/badge/agentskills.io-IBM%20API%20Connect-7C3AED?style=flat-square&labelColor=1a1a2e)](https://agentskills.io)
[![License](https://img.shields.io/badge/License-Apache%202.0-0062FF?style=flat-square&labelColor=1a1a2e)](LICENSE)
[![Skills](https://img.shields.io/badge/Skills-9-22c55e?style=flat-square&labelColor=1a1a2e)](skills)
[![IBM API Connect](https://img.shields.io/badge/IBM%20API%20Connect-Compatible-0062FF?style=flat-square&labelColor=1a1a2e)](https://www.ibm.com/docs/en/api-connect)

---

This repository brings together reusable skills and MCP servers for IBM API Connect Flow Pilot use cases across API authoring, Governance, Testing, Deployment, Lifecycle management, Analytics, and AI workflows. It also includes capabilities for building MCP servers and tools, creating LLM providers, exposing REST APIs as MCP, and enabling MCP proxying.


## What's available?

### Skills

| Skills | Description |
|---|---|
| [setup-agent-kit](skills/setup-agent-kit/SKILL.md) | One-time setup skill for configuring IBM API Connect Flow Pilot and required assets |
| [project-manager](skills/project-manager/SKILL.md) | Manage project CRUD for API development workflows |
| [build-project](skills/build-project/SKILL.md) | Build and compile projects into deployable artifacts |
| [lint-project](skills/lint-project/SKILL.md) | Analyze projects for syntax and policy errors; enforce style, conformance rules and security best practices |
| [publish-project](skills/publish-project/SKILL.md) | Publish projects to a specified catalog or deployment target|
| [asset-manager](skills/asset-manager/SKILL.md) | Manage authoring of API/AI assets and related artifacts |
| [test-generator](skills/test-generator/SKILL.md) | Manage authoring of API tests and test suites for automated validation |
| [rest-to-mcp-generator](skills/rest-to-mcp-generator/SKILL.md) | Builds MCP servers/tools for existing REST APIs |
| [operation-selector](skills/operation-selector/SKILL.md) | Select and map operations from an API specification to expose as MCP tools |
| [setup-mcp-asset](skills/setup-mcp-asset/SKILL.md) | Register a published and subscribed MCP asset into your agent — reads `subscriptions/*-creds.json` and writes the MCP server config entry automatically |

### MCP servers

| Server | Description | Tools |
---|---|---|
| [Management](mcp-servers/management) |Exposes tools for API Connect's management operations| List Consumer Orgs, List Consumer Apps, List Consumer App Credentials, Create Consumer App, List Subscriptions In Consumer App, List Subscriptions In A Catalog, Create Subscription For Published API, Create Subscription For Published Product, List Published Apis, List Published Products, Create Project, List Project Files, List Catalogs, List Spaces, List Gateways In Catalog, List Managed Projects, List LLM Providers, LLM Provider Generator |
| [Analytics](mcp-servers/analytics) | Exposes tools for analytics operations  | Get Analytics Status, Get Analytics Usage, Get Analytics Latency, Get Analytics Users, Get Analytics Consumer, Get Analytics Application, Get Analytics AI LLM, Get Analytics MCP |
| [Governance](mcp-servers/governance) | Exposes tools for linting and ruleset management in API Connect| Scan, Rescan, Get Scan, List Scans, Get Scan Report, Get All Rulesets, Validate OpenAPI, Validate Product, Validate With Rulesets, Rule Remediation, List Scan Reports, Create Scan Report, Update Scan Report, Delete Scan Report, Clear Scan Reports, Get Rules From Ruleset, Create Ruleset With Rule, Spectral Rule Validator, Download Scan Report Csv, Governance Ruleset Creator, Governance Ruleset Updater |
| [DataPower Interact Gateway](mcp-servers/ai-gateway-management) | Exposes tools for DataPower Interact Gateway in API Connect| List LLM Providers, LLM Provider Generator, Rest To MCP Generator, MCP Tools Enhancer, IDIG Publish Project, MCP Tools List, MCP To MCP Generator |
| [DataPower Interact Gateway - onPremise](mcp-servers/interact-gateway-onprem) | Exposes tools for DataPower Interact Gateway onPremise platform | List LLM Providers, LLM Provider Generator, Rest To MCP Generator, MCP Tools Enhancer, IDIG Publish Project, MCP Tools List, MCP To MCP Generator, Get Analytics MCP, Get Analytics AI LLM |



## Installation of skills

1. Download the IBM API Connect Flow Pilot package from:
   **https://www.ibm.com/resources/mrs/assets/DownloadList?source=WebMtds_FlowPilot&lang=en_US**

2. Unzip the downloaded package and navigate to the extracted folder:
   ```bash
   unzip <downloaded-file>.zip -d apic-flow-pilot
   cd apic-flow-pilot
   ```

3. Install the skills:
   ```bash
   # Install globally (available across all projects)
   npx skills add . -g

   # Install locally (available in current project only)
   npx skills add .
   ```

4. To install a specific skill only:
   ```bash
   npx skills add . --skill <skill-name>

   # Example
   npx skills add . --skill project-manager
   ```
---

## Configuring the MCP servers

```bash
# Install the setup skill (if not already installed)
npx skills add . --skill setup-agent-kit

# Once installed, execute the below prompt in the agent's chat
/setup-agent-kit
```

### Finding your credentials

The setup skill will ask which deployment type you are using and then guide you. Use the quick-reference below to locate each value before running the setup.

---

#### Software as a Service (SaaS)

| Credential | Where to find it |
|---|---|
| `APIC_MANAGEMENT_URL` | Use the regional URL that matches your instance (see table below) |
| `API_KEY` | Profile icon (top-right) → **My API Keys** → use an existing key or click **Add** with **Enable multiple use** checked |
| `APIC_PLATFORM_URL` | On the **My API Keys** page → **Authenticating for the platform REST API** section → base URL from the `curl` example, **without** the `/api/token` suffix |
| `client_id` / `client_secret` | Same **Authenticating for the platform REST API** `curl` block — values are in the request body |
| `PROVIDER_ORG` | Top-left breadcrumb in the API Manager header, e.g. `my-org` |

**Regional APIC Management URLs (SaaS)**

| Region | AWS Region | APIC Management URL |
|---|---|---|
| N. Virginia | us-east-1 | `https://api-manager.us-east-a.apiconnect.automation.ibm.com` |
| Frankfurt | eu-central-1 | `https://api-manager.eu-central-a.apiconnect.automation.ibm.com` |
| London | eu-west-2 | `https://api-manager.eu-west-a.apiconnect.automation.ibm.com` |
| Mumbai | ap-south-1 | `https://api-manager.ap-south-a.apiconnect.automation.ibm.com` |
| Sydney | ap-southeast-2 | `https://api-manager.ap-southeast-a.apiconnect.automation.ibm.com` |
| Jakarta | ap-southeast-3 | `https://api-manager.ap-southeast-b.apiconnect.automation.ibm.com` |

**Getting your API key and platform credentials (SaaS)**

1. Log in to your APIC Management URL.
2. Click the **profile icon** (your initials, top-right corner) → **My API Keys**.
3. Use an existing key or click **Add** → fill in a title/description, set a timeout, check **Enable multiple use**, then click **Create**.
4. On the same page, scroll to the **Authenticating for the platform REST API** section. The `curl` snippet shows the full token URL and the `client_id` / `client_secret` values. Strip `/api/token` from the URL to get `APIC_PLATFORM_URL`.

---

#### IBM webMethods Hybrid Integration (IWHI)

| Credential | Where to find it |
|---|---|
| `APIC_MANAGEMENT_URL` | Base URL of your API Manager in the IBM Technology Zone or Flow Pilot environment, e.g. `https://prod608833.m-yqb-c1.apiconnect.ipaas.test.automation.ibm.com` |
| `API_KEY` | Profile icon (top-right) → **My API Keys** → use an existing key or click **Add** with **Enable multiple use** checked |
| `APIC_PLATFORM_URL` | On the **My API Keys** page → **Authenticating for the platform REST API** section → base URL from the `curl` example, **without** the `/api/token` suffix, e.g. `https://platform-api.m-yqb.apiconnect.ipaas.test.automation.ibm.com` |
| `client_id` / `client_secret` | Same **Authenticating for the platform REST API** `curl` block — values are in the request body |
| `PROVIDER_ORG` | API Connect home page → **Settings** (left nav) → **Overview** → Organisation name |

**Getting your API key and platform credentials (IBM webMethods Hybrid Integration)**

1. Log in to your APIC Management URL.
2. Click the **profile icon** (your initials, top-right corner) → **My API Keys**.
3. Use an existing key or click **Add** → fill in a title/description, set a timeout, check **Enable multiple use**, then click **Create**.
4. On the same page, scroll to the **Authenticating for the platform REST API** section. The `curl` snippet shows the full token URL and the `client_id` / `client_secret` values. Strip `/api/token` from the URL to get `APIC_PLATFORM_URL`.

---

#### On-premises

| Credential | Where to find it |
|---|---|
| `APIC_MANAGEMENT_URL` | Base URL of your API Manager, e.g. `https://manager.studio2708.joker.dev.ciondemand.com` |
| `APIC_PLATFORM_URL` | Typically `https://api.<host>`, e.g. `https://api.studio2708.joker.dev.ciondemand.com` — confirm with your administrator if different |
| `PROVIDER_ORG` | Top-right corner of the API Manager header, e.g. `ibm` |
| `API_KEY` | Navigate to `<APIC_MANAGEMENT_URL>/manager/<PROVIDER_ORG>/apikeys` → use an existing key or click **Add** with **multiple use** enabled |
| `client_id` / `client_secret` | Home page → **Download Tools** → **Toolkit** → **Download** next to **Toolkit credentials** → open `credentials.json` and copy from the `toolkit` section |

**Getting `client_id` and `client_secret` (On-premises)**

1. From the API Manager **Home** page, click **Download Tools** in the "Get started" panel.
2. Select **Toolkit** on the left, then click **Download** next to **Toolkit credentials**.
3. Open the downloaded `credentials.json`. The values are in the **`toolkit`** section:

```json
{
  "toolkit": {
    "endpoint": "https://api.studio2708.joker.dev.ciondemand.com/api",
    "client_id": "<your-client-id>",
    "client_secret": "<your-client-secret>"
  }
}
```

---

## Compatible AI Agents

| Agent | Supported |
|---|---|
| IBM Bob | ✅ |
| Claude Code | ✅ |
| GitHub Copilot (VS code) | ✅ |
| Any agent supporting skills.sh | ✅ |

---

## Dependencies

- **Node.js 24** — required by the `apic` CLI
- **`@apistudio/apim-cli`** — Can also be installed with `npm i -g @apistudio/apim-cli@latest`
- **IBM API Connect instane access** — required for publishing and testing assets

---

## FAQ

**How do I install a specific skill?**
```bash
npx skills add . --skill project-manager
```

**Which agents support these skills?**
Any agent that supports the [skills.sh](https://skills.sh) ecosystem.

**How do I report a problem?**
Open an issue in this repository with the skill name and a description of the unexpected behavior.

**Can I contribute?**
Yes — contributions are welcome. See the skill directories for structure and format examples, then submit a pull request.

---
## Blogs

 - [IBM API Connect MCP Server](https://community.ibm.com/community/user/blogs/goutham-shivanna/2026/01/26/ibm-api-connect-mcp-server)
 - [Exploring IBM API Connect v12.1.0 API Analytics with the API Agent's Analytics MCP Tool](https://community.ibm.com/community/user/blogs/michael-osullivan/2025/12/23/apic-api-analytics-with-the-api-agent)

## Documentation
- [IBM API Connect Documentation](https://www.ibm.com/docs/en/api-connect)
- [IBM DataPower Interact Gateway Documentation](https://www.ibm.com/docs/en/dp-interact-gateway/12.1.1)
- [IBM API Connect Product Page](https://www.ibm.com/products/api-connect)

## External resources
- [skills.sh](https://skills.sh)
- [agentskills.io](https://agentskills.io)

---

## License

See the repository license for information about usage terms and restrictions.
