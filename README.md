![Logo](media/logos/socialjsonfield-3d.png)

# SocialJSONField

> A portable schema for describing multiple social media accounts per entity using a standardized JSON format.  

SocialJSONField defines a proposed convention for representing **multiple social media accounts** (including more than one per platform) within a single JSON field. The goal is to enable a **consistent, framework-agnostic** way to store and exchange this kind of data across programming languages, databases, APIs, and serialization layers.

---

## 🔧 Why SocialJSONField?

Developers often need to store and expose social media account information — for users, organizations, projects, or brands. However, there's no agreed-upon structure for storing this information compactly while supporting:

- Multiple accounts per platform (e.g., personal and business Instagram)
- Verified status or metadata
- Easy hyperlink generation
- Frontend-friendly usage
- Compatibility across ORM frameworks like Django, Rails, Sequelize, etc.

**SocialJSONField provides a schema and best-practice convention to solve this.**

---

## 📦 Basic Structure

```json
{
  "accounts": [
    {
      "platform": "instagram",
      "label": "personal",
      "handle": "tony123",
      "uri_template": "https://instagram.com/{handle}",
      "verified": false,
      "meta": {
        "followers": 1200,
        "created_at": "2020-03-01"
      }
    }
  ]
}
```

---

## 🧱 Field Reference

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `platform` | `string` | ✅ | Social platform name (e.g., `instagram`, `tiktok`, `linkedin`) |
| `label` | `string` | ⭕️ | User-defined context (e.g., `personal`, `photography`, `work`) |
| `handle` | `string` | ✅ | Platform-specific username or ID (without `@`) |
| `uri_template` | `string` | ✅ | A URI template containing `{handle}` placeholder |
| `verified` | `boolean` | ⭕️ | Whether the account is officially verified |
| `meta` | `object` | ⭕️ | Optional metadata (e.g., followers, bio, timestamps) |

---

## ✨ Usage Examples

### ➤ User with multiple Twitter accounts

```json
{
  "accounts": [
    {
      "platform": "twitter",
      "label": "personal",
      "handle": "jane_doe",
      "uri_template": "https://twitter.com/{handle}",
      "verified": true
    },
    {
      "platform": "twitter",
      "label": "work",
      "handle": "jane_at_acme",
      "uri_template": "https://twitter.com/{handle}",
      "verified": false
    }
  ]
}
```

---

### ➤ NGO profile with Instagram and LinkedIn

```json
{
  "accounts": [
    {
      "platform": "instagram",
      "label": "photos",
      "handle": "greenfutureorg",
      "uri_template": "https://instagram.com/{handle}"
    },
    {
      "platform": "linkedin",
      "handle": "company/greenfuture",
      "uri_template": "https://linkedin.com/in/{handle}"
    }
  ]
}
```

---

### ➤ Company page with extra metadata

```json
{
  "accounts": [
    {
      "platform": "facebook",
      "handle": "acmeofficial",
      "uri_template": "https://facebook.com/{handle}",
      "meta": {
        "followers": 50400,
        "page_type": "brand"
      }
    }
  ]
}
```

---

## 💻 Intended Usage

### ✅ Use this schema if:

- You need to store social media info for users, companies, creators, etc.
- You want to support **multiple profiles per platform**
- You’re building JSON APIs, mobile apps, dashboards, or admin tools
- You want consistency across languages and data stores

### ❌ Avoid using this schema if:

- You only need a fixed set of fields (e.g., `twitter_url`, `linkedin_url`)
- Your app does not handle dynamic or user-generated content
- You already use an external identity service or OAuth provider with direct integrations

---

## 🌐 Integration Tips

### In Django / Python

```python
from django.db import models
from django.contrib.postgres.fields import JSONField

class UserProfile(models.Model):
    social = JSONField()  # store according to SocialJSONField schema
```

### In JavaScript / TypeScript

```ts
type SocialAccount = {
  platform: string;
  label?: string;
  handle: string;
  uri_template: string;
  verified?: boolean;
  meta?: Record<string, any>;
};

type SocialJSONField = {
  accounts: SocialAccount[];
};
```

### In API Docs (OpenAPI 3)

```yaml
SocialAccount:
  type: object
  required: [platform, handle, uri_template]
  properties:
    platform:
      type: string
    label:
      type: string
    handle:
      type: string
    uri_template:
      type: string
    verified:
      type: boolean
    meta:
      type: object
      additionalProperties: true
```

---

## 🧪 Validating Your Data

A formal JSON Schema will be provided in [`schema/social-accounts.schema.json`](schema/social-accounts.schema.json).  
You will be able to use tools like [AJV](https://ajv.js.org/), [`jsonschema`](https://pypi.org/project/jsonschema/), or online validators to check conformance.

---

## 📌 Roadmap

- [x] Initial JSON schema definition
- [ ] Examples folder
- [ ] JS + Python validation libs
- [ ] Django/Rails plugins
- [ ] GitHub Pages site
- [x] Logo & identity
- [ ] Outreach to OSS maintainers

---

## 📢 Call for Contributions

We welcome help building:

- Validators in your favorite language
- Integration examples (Django, Rails, Laravel, etc.)
- Schema suggestions or edge case examples
- Real-world adoption or feedback

Fork the repo and send us a pull request, or open an issue to start a discussion.

---

## 📄 License

MIT License – feel free to use and contribute.

---

## 🔗 Related Projects & Inspiration

- [`package.json`](https://docs.npmjs.com/cli/v9/configuring-npm/package-json)
- [`robots.txt`](https://www.robotstxt.org/)
- [`OpenAPI`](https://www.openapis.org/)
- [`h-card`](https://microformats.org/wiki/h-card)

---

Made with ❤️ from 🇵🇪 by [Antonio Ognio](https://github.com/aognio) and the SocialJSONField community.
