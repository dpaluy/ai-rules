---
description: Security analysis configuration with Brakeman
globs: bin/brakeman
alwaysApply: false
---
 # Brakeman Security Analysis Standards

## Context
- Applied when configuring or running security analysis
- Used for identifying security vulnerabilities in Rails applications
- Referenced during security reviews and audits

## Requirements
- Run Brakeman as part of the CI/CD pipeline
- Maintain a configuration file for consistent scans
- Document false positives with clear justifications
- Address high-risk vulnerabilities immediately
- Review security reports regularly

## Configuration Guidelines

### Core Setup
- Install Brakeman as a development dependency
- Configure to scan all relevant application code
- Set appropriate confidence levels for reporting
- Exclude test files and vendor code

### False Positive Management
- Document false positives in a configuration file
- Include justification for each ignored warning
- Review ignored warnings periodically
- Use specific ignore patterns rather than broad ones

### Vulnerability Handling
- Categorize vulnerabilities by risk level
- Address high-risk issues before deployment
- Create tickets for medium-risk issues
- Document mitigation strategies for accepted risks

## Examples

<example>
# Good: Well-configured Brakeman setup
# .brakeman.yml
---
:ignore_file: .brakeman.ignore
:skip_files:
  - app/controllers/test
:skip_checks:
  - CrossSiteScripting # Handled by Content Security Policy
:output_files:
  - tmp/brakeman-report.html
:min_confidence: 2
</example>

<example type="invalid">
# Bad: Poorly configured Brakeman setup
# .brakeman.yml
---
:skip_checks:
  - All # Disables all checks
:min_confidence: 0 # Reports everything, including low confidence
</example>

## Integration Guidelines
- Run Brakeman in CI/CD pipeline
- Generate HTML reports for readability
- Configure exit codes for CI/CD integration
- Set up notifications for new vulnerabilities
- Integrate with code review process

metadata:
  priority: high
  version: 1.0