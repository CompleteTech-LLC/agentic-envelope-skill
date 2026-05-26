---
name: agentic-envelope-skill
description: Generate branded CompleteTech LLC printable #10 addressed envelope PDFs and delivery packages with sender, recipient, optional attention line, postage box text, return-address toggle, logo, brand palette, attachment manifests, filenames, recipient metadata, and delivery-readiness checks. Use when Codex needs to package contracts, certificates, invoices, proposals, notices, or other CompleteTech artifacts for mailing or external delivery.
version: 1.0.0
metadata:
  openclaw:
    skillKey: agentic-envelope-skill
    homepage: https://github.com/CompleteTech-LLC/agentic-envelope-skill
    requires:
      bins:
        - python3
    install:
      - kind: uv
        package: pyyaml>=6.0
      - kind: uv
        package: reportlab>=4.0
---

# Agentic Envelope Skill

## Purpose

Generate branded CompleteTech LLC #10 addressed envelope PDFs and delivery package metadata.

## System Boundary

This skill owns packaging, addressed envelopes, recipient metadata, attachment lists, output filenames, delivery-readiness checks, and mailing/delivery notes. It does not write the contract, proposal, invoice, certificate, proof asset, delivery record, or email body. Use the orchestrator to decide when this skill is needed, and use `agentic-security-review-skill` before packaging sensitive attachments or external-action workflows.

## Resource Guide

- `generate_envelope.py` - self-contained envelope generator.
- `config.ini` - provider, recipient, branding, and envelope defaults.
- `examples/client_address_override.ini` - recipient address override example.
- `assets/logo.png` - envelope header logo.

## Required Inputs

For a normal envelope run, collect:

1. recipient name or organization
2. recipient mailing address
3. optional attention line
4. artifact paths or attachment names when creating a delivery package
5. delivery mode: physical mail, digital attachment package, or internal archive

Provider return address, branding, postage box text, and print-layout defaults come from config unless the user asks to override them.

## Outputs

- Envelope PDF path when physical mailing is requested.
- Attachment/package manifest with artifact names, recipients, and intended delivery mode.
- Recommended filenames for generated artifacts when useful.
- Missing recipient, address, attachment, or approval facts.
- Delivery-readiness note: draft, ready for review, approved to send, or blocked.

## Quality Rules

- Do not invent recipient names, mailing addresses, email addresses, or approval status.
- Do not package sensitive attachments for external delivery until recipient and approval status are verified.
- Keep business content in the source skill: contracts, invoices, certificates, proposals, proof, and email copy stay outside this skill.
- Use `TBD` or ask for missing delivery facts instead of guessing.

## How to Run

```bash
pip install -r requirements.txt
python generate_envelope.py \
  --config config.ini examples/client_address_override.ini \
  --out output/acme_envelope.pdf
```

## Agent Operating Guidance

1. Confirm or collect the recipient organization/name and full mailing address.
2. Create or update an override INI instead of editing source defaults for one-off recipients.
3. Run `generate_envelope.py --config config.ini <override.ini> --out output/<recipient_slug>_envelope.pdf`.
4. Use `--no-return-address` only when the user asks to omit the sender address.
5. If packaging multiple artifacts, return a manifest with artifact path, recipient, delivery mode, approval status, and missing facts.
6. Return the generated PDF path and remind the user to print at 100% scale when physical mailing is requested.

## Certificate Receipt Guidance

The skill remains usable without a classroom key. When certificate credit is needed, use `scripts/request_receipt.py` after the skill run. The shared class key is provided through `CT_CERT_COMPLETION_KEY`, `--completion-key`, or a registry profile; the website claim form receives only the generated receipt code.

Receipt requests include this skill ID: `agentic-envelope-skill`. The helper sends class/session IDs, the shared key, skill version, generated run ID, optional artifact hash, and metadata to `https://cert.complete.tech/api/skill-runs`. The student claims the certificate at `https://cert.complete.tech/claim` with the returned receipt.

Do not print, store, or commit real classroom completion keys.
