# Data Notice

## Purpose

This repository is a technical sample for the [Romania e-Factura Validator API](https://apify.com/kamerozkan/romania-efactura-validator). It contains three real dataset rows and the corresponding standalone JSON Schema.

The Actor and this repository are independent, unofficial products. They are not affiliated with, sponsored by, or endorsed by ANAF, Romania's Ministry of Finance, any invoice recipient, or any upstream validation project.

## Provenance snapshot

The three JSON records were retrieved on 2026-07-29 from successful Apify run `OdBixrTgdWyEU9wY6`, build `0.0.3` (`DpQXkcSU1bwHQYqpx`), dataset `mOxicFvIjtvKqBxDK`.

- `01_live_accepted_output.json` is an `ACCEPTED` result for a synthetic CIUS-RO UBL fixture.
- `02_live_rejected_output.json` is a `REJECTED` result with arithmetic consistency findings.
- `03_live_not_evaluated_output.json` is a `NOT_EVALUATED` result for an unsupported CII syntax.

The JSON files are verbatim dataset records. No field was reconstructed, inferred, or edited.

## Privacy and security

This repository contains no customer invoice, raw XML, base64 document, access token, cookie, signed URL, webhook URL, email address, bank detail, tax identifier, or customer account identifier.

The accepted and rejected input fixtures are project-authored synthetic documents. The output rows expose technical metadata and findings, not invoice parties, line items, payment details, or full invoice bodies.

Customer validation findings and optional reports can contain invoice values. Users remain responsible for lawful processing, access control, retention, deletion, and applicable privacy, tax, accounting, database, and contractual requirements.

## Interpretation limits

- `ACCEPTED` means the submitted bytes passed the pinned offline XSD and Schematron checks.
- `REJECTED` means the document was evaluated and at least one required technical rule failed.
- `NOT_EVALUATED` means a processing or safety failure prevented a technical decision.
- A result does not prove ANAF acceptance, legal or tax validity, issuer identity, authenticity, signature validity, delivery, payment, or recipient acceptance.
- A future ruleset update can change findings for the same source bytes.

## License boundary

The MIT License applies only to the original documentation, JSON output samples, and JSON Schema committed here.

It does not relicense CIUS-RO, EN 16931, UBL, Romanian rule artifacts, specifications, third-party software, names, marks, or report formats. Review upstream licenses and terms before redistribution or commercial use.
