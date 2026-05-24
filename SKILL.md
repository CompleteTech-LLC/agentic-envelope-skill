---
name: agentic-envelope-skill
description: Generate branded CompleteTech LLC printable #10 addressed envelope PDFs with sender, recipient, optional attention line, postage box text, return-address toggle, logo, and brand palette. Use when Codex needs to create mailing envelopes for contracts, certificates, invoices, notices, or other CompleteTech artifacts.
---

# Agentic Envelope Skill

## Purpose

Generate a branded CompleteTech LLC #10 addressed envelope PDF.

## Files

- `generate_envelope.py` - self-contained envelope generator.
- `config.ini` - provider, recipient, branding, and envelope defaults.
- `examples/client_address_override.ini` - recipient address override example.
- `assets/logo.png` - envelope header logo.

## Required Inputs

For a normal envelope run, collect:

1. recipient name or organization
2. recipient mailing address
3. optional attention line

Provider return address, branding, postage box text, and print-layout defaults come from config unless the user asks to override them.

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
5. Return the generated PDF path and remind the user to print at 100% scale.
