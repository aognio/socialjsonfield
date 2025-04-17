# Changelog

All notable changes to this project will be documented in this file.

This project adheres to [Semantic Versioning](https://semver.org/).

---

## [1.0.0] - 2025-04-17

🎉 First public release of **SocialJSONField**!

### Added
- Initial JSON schema to define the structure of `accounts`
- Support for multiple accounts per platform (e.g., Instagram: personal & photography)
- Required fields: `platform`, `handle`, `uri_template`
- Optional fields: `label`, `verified`, `meta`
- README with purpose, schema, and integration examples
- platforms.json file with canonical slugs and URI templates
- Sample JSON files in the `examples/` folder
- Basic repo structure for future package implementations
- Call for contributions to framework-specific validators (Django, Rails, etc.)
- GitHub Pages compatibility for upcoming website

---

## Future plans (Unreleased)

### Planned
- Add unit tests and linting for schema validation
- Publish the JSON Schema on SchemaStore.org or similar
- Implement CLI validator (`socialjson validate`)
- Add implementations in:
  - Python (pydantic)
  - JavaScript (AJV)
  - Go (struct + validation)
- Create a visual logo and favicon
- Enable optional `@` symbol hint in meta or presentation layer
- Document usage patterns for apps, organizations, events

---

