# Data Notice

## Purpose

This repository is the public technical release preview for the private `romania-efactura-validator` Actor. It contains three real dataset rows, three matching runnable input definitions, their synthetic XML fixtures, and the corresponding standalone JSON Schema. The Actor is not currently available through the public Apify Store.

The Actor and this repository are independent, unofficial products. They are not affiliated with, sponsored by, or endorsed by ANAF, Romania's Ministry of Finance, any invoice recipient, or any upstream validation project.

## Provenance snapshot

The three JSON records were retrieved on 2026-07-29 from successful Apify run `OdBixrTgdWyEU9wY6`, build `0.0.3` (`DpQXkcSU1bwHQYqpx`), dataset `mOxicFvIjtvKqBxDK`.

The latest private hosted build was separately verified as `0.0.4` `SUCCEEDED` on 2026-07-30. Exact `invoice-validated` pricing at `$0.004` is configured, but the Store publication attempt was blocked by the account's daily publication quota. This repository does not claim public Actor availability.

- `01_live_accepted_output.json` is an `ACCEPTED` result for a synthetic CIUS-RO UBL fixture.
- `02_live_rejected_output.json` is a `REJECTED` result with arithmetic consistency findings.
- `03_live_not_evaluated_output.json` is a `NOT_EVALUATED` result for an unsupported CII syntax.

The JSON files are verbatim dataset records. No field was reconstructed, inferred, or edited.

## Runnable input provenance

- [`01_accepted_input.json`](01_accepted_input.json) references the committed `valid_invoice.xml` fixture; SHA-256 `4a51789dc322ccbdbfa8066e7b313971842a7c53e57e70957de453c4a5b99c4a`.
- [`02_rejected_input.json`](02_rejected_input.json) references the committed `invalid_totals.xml` fixture; SHA-256 `db8b2bc2b631db1e12416cbc4885bca3893e6f9c6066705a7284ef76cb348f86`.
- [`03_not_evaluated_input.json`](03_not_evaluated_input.json) references the committed unsupported CII fixture used to demonstrate the syntax boundary.

The first two digests match their corresponding real output rows. The linked input files become runnable from their raw GitHub URLs when this repository refresh is published; that does not make the private Actor publicly runnable.

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
