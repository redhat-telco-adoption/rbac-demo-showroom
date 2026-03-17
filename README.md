# OpenShift RBAC Demo -- Showroom Guide

Presenter-led demo guide for the OpenShift RBAC demo, built with [Antora](https://antora.org) and the [RHDP Showroom theme](https://github.com/rhpds/rhdp_showroom_theme).

## Structure

```
showroom/
├── site.yml                          # Antora site configuration
├── content/
│   ├── antora.yml                    # Antora component descriptor
│   └── modules/ROOT/
│       ├── nav.adoc                  # Sidebar navigation
│       └── pages/
│           ├── index.adoc            # Facilitator guide (start here)
│           ├── 01-overview.adoc      # Business context & VMware mapping
│           ├── 02-details.adoc       # Timing, credentials, troubleshooting
│           ├── 03-foundation.adoc    # Scenarios 0-1: platform view & isolation
│           ├── 04-access.adoc        # Scenarios 2-3: delegation & custom roles
│           ├── 05-security.adoc      # Scenarios 4-5: auditor & CI/CD SA
│           ├── 06-advanced.adoc      # Scenarios 6-8: cross-ns, groups, quotas
│           ├── 07-extended.adoc      # Scenarios 9-10: aggregation & audit log
│           └── 99-conclusion.adoc    # Wrap-up & next steps
```

## Building locally

### Prerequisites

- [Node.js](https://nodejs.org) 18+
- Antora CLI

Install Antora globally:

```bash
npm install -g @antora/cli @antora/site-generator
```

### Build

From the `showroom/` directory:

```bash
antora site.yml
```

Output is written to `showroom/www/`. Open `www/index.html` in a browser to preview.

```bash
open www/index.html        # macOS
xdg-open www/index.html    # Linux
```

### Live preview

For a local server with auto-refresh, use [`http-server`](https://www.npmjs.com/package/http-server):

```bash
npm install -g http-server
http-server www/
```

Then open `http://localhost:8080`.

## Deploying on RHDP (Showroom)

This bundle is designed for the Red Hat Demo Platform Showroom framework.

1. Push this repository to GitHub.
2. In the RHDP catalog item configuration, set the Showroom content source to point to this repository and `showroom/` as the content path.
3. RHDP will run `antora site.yml` during provisioning and serve the output.

The `{openshift_console_url}` and `{openshift_api_url}` placeholders in the content are substituted at build time by RHDP with the actual environment URLs.

## UI theme

This guide uses the `patternfly-6` release of the RHDP Showroom theme:

```
https://github.com/rhpds/rhdp_showroom_theme/releases/tag/patternfly-6
```

To switch themes, update the `ui.bundle.url` in `site.yml`.

## Before running the demo

The demo environment must be deployed before using this guide. From the repo root:

```bash
cd rbac-demo/
./scripts/deploy.sh
./scripts/validate.sh   # must exit 0
```

See `02-details.adoc` (Demo Details) for the full pre-flight checklist and troubleshooting guide.
