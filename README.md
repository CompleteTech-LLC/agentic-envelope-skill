<div align="center">

<img src="assets/logo.png" alt="CompleteTech LLC" width="220"/>

# Agentic Envelope Skill

**A CompleteTech LLC envelope generator - from mailing details to branded, printable #10 addressed envelopes.**

![Python 3.10+](https://img.shields.io/badge/python-3.10%2B-3776AB?logo=python&logoColor=white)
![License MIT](https://img.shields.io/badge/license-MIT-green)
![Providers CompleteTech](https://img.shields.io/badge/providers-CompleteTech-8A2BE2)
![Format PDF](https://img.shields.io/badge/format-PDF-B91C1C)

</div>

---

This skill generates CompleteTech-branded #10 addressed envelope PDFs with a logo, return address, recipient block, attention line, postage box, and print-at-100-percent footer note. It is built for mailing contracts, certificates, notices, and other artifacts that need consistent CompleteTech presentation.

## Quick Start

```bash
pip install -r requirements.txt

# Use the default recipient from config.ini.
python generate_envelope.py

# Generate using a per-recipient override file.
python generate_envelope.py \
  --config config.ini examples/client_address_override.ini \
  --out output/acme_envelope.pdf

# Omit return address for one run.
python generate_envelope.py --no-return-address
```

The default output path is `output/addressed_envelope.pdf`.

## Inputs

The generator reads these INI sections:

| Section | Purpose |
|---|---|
| `provider` | Return-address name and mailing address |
| `client` | Recipient name and mailing address |
| `branding` | Logo path, brand name, tagline, and color palette |
| `envelope` | Attention line, postage-box text, return-address toggle, footer note |

Pass multiple config files with `--config`; later files override earlier files.

## Assets

- `assets/logo.png` - envelope header logo.

## Source

This standalone skill was extracted from the envelope generator originally bundled in `CompleteTech-LLC/agentic-contract-skill`.
