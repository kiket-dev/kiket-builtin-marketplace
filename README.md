# Kiket Marketplace

This directory contains the marketplace catalog content for Kiket - curated bundles, category definitions, and assets.

## Directory Structure

```
marketplace/
├── README.md           # This file
├── categories.yaml     # Category definitions with icons and colors
├── bundles/           # Solution bundle definitions
│   ├── customer_support.yaml
│   ├── developer_toolkit.yaml
│   └── marketing_suite.yaml
└── assets/            # Bundle icons, screenshots, etc.
```

## Bundles

Bundles are curated solution packages that combine templates, extensions, and analytics into ready-to-use solutions.

### Bundle Schema

```yaml
id: unique_bundle_id
name: Human Readable Name
description: |
  Multi-line description of the bundle and its use cases.
version: "1.0.0"

category: operations|marketing|development|suite
tags:
  - relevant
  - tags

featured: true|false

contents:
  templates:
    - template_slug      # References definitions/*/
  extensions:
    - dev.kiket.ext.id   # References extensions/*/
  analytics: []          # Future: dashboard/report templates

requirements:
  min_plan: free|starter|professional|enterprise

maintainer: Kiket|Partner Name
documentation: https://docs.kiket.dev/bundles/bundle-id
license: MIT
```

### Available Bundles

| Bundle | Category | Templates | Extensions | Min Plan |
|--------|----------|-----------|------------|----------|
| Customer Support | Operations | ecommerce | email, slack, teams, twilio | Professional |
| Developer Toolkit | Development | scrum | github, slack | Professional |
| Marketing Suite | Marketing | kanban | email, slack, make | Professional |

## Categories

Categories are defined in `categories.yaml` and used to organize:
- Extension repositories
- Definition (template) repositories
- Marketplace bundles

### Available Categories

| ID | Name | Description |
|----|------|-------------|
| project_management | Project Management | Tools for managing projects, sprints, and workflows |
| marketing | Marketing | Campaign management and marketing automation |
| development | Development | Software development tools and CI/CD |
| communication | Communication | Email, chat, and notifications |
| automation | Automation | Workflow automation platforms |
| productivity | Productivity | Time tracking and efficiency tools |
| operations | Operations | Order management and fulfillment |
| suite | Solution Suites | Complete solution bundles |

## Syncing

The marketplace catalog is synced to the database using:

```bash
# Sync all marketplace content
bundle exec rails marketplace:sync

# List current catalog
bundle exec rails marketplace:list

# Validate bundle references
bundle exec rails marketplace:validate
```

During deployment, the `marketplace-sync` Cloud Run job automatically syncs the catalog after migrations.

## Adding New Bundles

1. Create a new YAML file in `bundles/` following the schema above
2. Ensure all referenced templates exist in `definitions/`
3. Ensure all referenced extensions exist in `extensions/`
4. Run `bundle exec rails marketplace:validate` to check references
5. Commit to the marketplace submodule
6. Update the parent repo's submodule reference

## Plan Levels

| Plan | Description |
|------|-------------|
| free | Available to all users |
| starter | Basic paid features |
| professional | Advanced features for growing teams |
| enterprise | Full platform with dedicated support |

## License

MIT License - See LICENSE file for details.
