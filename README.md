> **Release preview:** The Actor is private and not currently runnable from the public Apify Store. This repository documents the verified release candidate.

# Romania e-Factura Validator API: Samples and JSON Schema

![Release](https://img.shields.io/badge/Actor-private%20release%20preview-F59E0B)
![Latest build](https://img.shields.io/badge/latest_build-0.0.4%20SUCCEEDED-2f855a)
![Validation](https://img.shields.io/badge/scope-OFFLINE__PREFLIGHT-0057a8)
![Rules](https://img.shields.io/badge/CIUS--RO-1.0.1-0057a8)
![Samples](https://img.shields.io/badge/live%20samples-3-2f855a)
![JSON Schema](https://img.shields.io/badge/schema-2020--12-4c1)
![License](https://img.shields.io/badge/license-MIT-blue)

Validate Romanian e-Factura UBL Invoice and CreditNote XML before submission. Each evaluated document returns a deterministic technical result, structured findings, SHA-256 evidence, and the exact pinned rule versions.

This repository contains three real output rows from one successful Actor run and the machine-readable contract in [`dataset_record.schema.json`](dataset_record.schema.json).

> **Decision boundary:** `ACCEPTED` means the submitted XML passed the pinned offline XSD and Schematron checks. It is not ANAF, legal, tax, accounting, authenticity, delivery, signature, or recipient acceptance evidence.

## Why this pipeline

| Need | Generic XML parser | This validator |
|---|---|---|
| UBL structure | XML syntax only | Pinned OASIS UBL 2.1 XSD |
| Romanian rules | Usually absent | CIUS-RO `1.0.1` and ro16931-ubl `1.0.9` |
| Arithmetic errors | Manual inspection | Structured rule ID and location |
| Audit evidence | Ad hoc text | Findings, source hash, pinned versions |
| Batch failures | One error can stop a batch | One independent result per document |
| Unsafe or unsupported source | Ambiguous error | Explicit `NOT_EVALUATED` result |

## Result contract

| Processing | Conformance | Meaning | `invoice-validated` billing |
|---|---|---|---|
| `SUCCEEDED` | `ACCEPTED` | Every required pinned technical layer passed | Charged |
| `SUCCEEDED` | `REJECTED` | At least one required technical rule failed | Charged |
| `FAILED` | `NOT_EVALUATED` | No technical decision was possible | Not charged |

The Actor charges `$0.004` per evaluated document. A platform Actor-start event can also apply. Check the current Store page before production use.

## Runnable input examples

| Input | Matching real output | Expected decision |
|---|---|---|
| [`01_accepted_input.json`](01_accepted_input.json) | [`01_live_accepted_output.json`](01_live_accepted_output.json) | `ACCEPTED` |
| [`02_rejected_input.json`](02_rejected_input.json) | [`02_live_rejected_output.json`](02_live_rejected_output.json) | `REJECTED` |
| [`03_not_evaluated_input.json`](03_not_evaluated_input.json) | [`03_live_not_evaluated_output.json`](03_live_not_evaluated_output.json) | `NOT_EVALUATED` |

The three project-authored synthetic XML fixtures are committed under [`fixtures/`](fixtures/). The accepted and rejected fixture hashes match the real output rows.

## Real output examples

All three records below are verbatim rows from successful run `OdBixrTgdWyEU9wY6`, build `0.0.3`, dataset `mOxicFvIjtvKqBxDK`.

Latest hosted build `0.0.4` was verified `SUCCEEDED` on 2026-07-30. The Actor has exact live `invoice-validated` pricing at `$0.004` but remains private because the account publication quota blocked its Store release. The sample rows remain attributed to build `0.0.3`.

<details>
<summary><strong>01. ACCEPTED</strong> - synthetic CIUS-RO UBL invoice</summary>

[`01_live_accepted_output.json`](01_live_accepted_output.json)

```json
{
  "inputIndex": 0,
  "documentId": "ro-valid",
  "fileName": "valid_invoice.xml",
  "processingStatus": "SUCCEEDED",
  "conformanceStatus": "ACCEPTED",
  "previewConformanceStatus": "NOT_EVALUATED",
  "validationScope": "OFFLINE_PREFLIGHT",
  "externalStateStatus": "NOT_EVALUATED_EXTERNAL_STATE",
  "rulesetEffectiveAt": "2024-06-05",
  "sourceFormat": "XML",
  "validationFamily": "ROMANIA_EFACTURA_CIUS_RO",
  "syntax": "UBL_INVOICE",
  "profile": "CIUS_RO_1_0_1",
  "scenario": "Romania e-Factura CIUS-RO 1.0.1 UBL Invoice",
  "versions": {
    "ubl": "2.1",
    "ciusRo": "1.0.1",
    "roSchematron": "1.0.9",
    "embeddedEn16931": "1.3.8",
    "saxonHe": "10.9",
    "saxonHeSha256": "491d8edf4ec811d15c2b2417b007218b9b938f15e4dfbad004025beb4e70e960",
    "compiledSchematronSha256": "3088b39e24dab440dc98b55cb4ba6845a5fd22b382da1f376f592ee6e0d0f2eb",
    "temurinJreImage": "eclipse-temurin:21-jre-jammy@sha256:d63bd8d9b171999cbed8576f2c76e874dd4856791a358536e5c4d407e77edc13",
    "schematronSkeleton": "02f3707b194ce5792bf77b14a66d782c060abba3",
    "roRulesArchiveSha256": "818e7dd77e429f5dbde7c60b43dddbdf1a9a82a1773c359caa80a36ef89ea7f2",
    "ublArchiveSha256": "60b80d76394a8a2add90723ecb8e0e2e9d826775de9749df37a72d60703f86ed",
    "activeRuleset": {
      "name": "CIUS-RO 1.0.1 / ro16931-ubl 1.0.9",
      "effectiveAt": "2024-06-05"
    },
    "artifactManifestSha256": "39add0e63650bd7ee218eaeae8459ee912331280be57ee686815977dd7e404ce"
  },
  "counts": {
    "fatal": 0,
    "error": 0,
    "warning": 0,
    "information": 0
  },
  "findings": [],
  "findingsTruncated": false,
  "previewCounts": {
    "fatal": 0,
    "error": 0,
    "warning": 0,
    "information": 0
  },
  "previewFindings": [],
  "previewFindingsTruncated": false,
  "sha256": "4a51789dc322ccbdbfa8066e7b313971842a7c53e57e70957de453c4a5b99c4a",
  "embeddedXmlSha256": null,
  "container": null,
  "checkedAt": "2026-07-29T11:24:48.006471Z",
  "reports": {},
  "error": null
}
```

</details>

<details>
<summary><strong>02. REJECTED</strong> - arithmetic consistency failures</summary>

[`02_live_rejected_output.json`](02_live_rejected_output.json)

```json
{
  "inputIndex": 1,
  "documentId": "ro-invalid",
  "fileName": "invalid_totals.xml",
  "processingStatus": "SUCCEEDED",
  "conformanceStatus": "REJECTED",
  "previewConformanceStatus": "NOT_EVALUATED",
  "validationScope": "OFFLINE_PREFLIGHT",
  "externalStateStatus": "NOT_EVALUATED_EXTERNAL_STATE",
  "rulesetEffectiveAt": "2024-06-05",
  "sourceFormat": "XML",
  "validationFamily": "ROMANIA_EFACTURA_CIUS_RO",
  "syntax": "UBL_INVOICE",
  "profile": "CIUS_RO_1_0_1",
  "scenario": "Romania e-Factura CIUS-RO 1.0.1 UBL Invoice",
  "versions": {
    "ubl": "2.1",
    "ciusRo": "1.0.1",
    "roSchematron": "1.0.9",
    "embeddedEn16931": "1.3.8",
    "saxonHe": "10.9",
    "saxonHeSha256": "491d8edf4ec811d15c2b2417b007218b9b938f15e4dfbad004025beb4e70e960",
    "compiledSchematronSha256": "3088b39e24dab440dc98b55cb4ba6845a5fd22b382da1f376f592ee6e0d0f2eb",
    "temurinJreImage": "eclipse-temurin:21-jre-jammy@sha256:d63bd8d9b171999cbed8576f2c76e874dd4856791a358536e5c4d407e77edc13",
    "schematronSkeleton": "02f3707b194ce5792bf77b14a66d782c060abba3",
    "roRulesArchiveSha256": "818e7dd77e429f5dbde7c60b43dddbdf1a9a82a1773c359caa80a36ef89ea7f2",
    "ublArchiveSha256": "60b80d76394a8a2add90723ecb8e0e2e9d826775de9749df37a72d60703f86ed",
    "activeRuleset": {
      "name": "CIUS-RO 1.0.1 / ro16931-ubl 1.0.9",
      "effectiveAt": "2024-06-05"
    },
    "artifactManifestSha256": "39add0e63650bd7ee218eaeae8459ee912331280be57ee686815977dd7e404ce"
  },
  "counts": {
    "fatal": 2,
    "error": 0,
    "warning": 0,
    "information": 0
  },
  "findings": [
    {
      "severity": "FATAL",
      "stage": "BUSINESS_RULE",
      "ruleId": "BR-CO-10",
      "message": "[BR-CO-10]-Sum of Invoice line net amount (BT-106) = Σ Invoice line net amount (BT-131).",
      "location": "/*:Invoice[namespace-uri()='urn:oasis:names:specification:ubl:schema:xsd:Invoice-2'][1]/*:LegalMonetaryTotal[namespace-uri()='urn:oasis:names:specification:ubl:schema:xsd:CommonAggregateComponents-2'][1]",
      "test": "(xs:decimal(cbc:LineExtensionAmount) = xs:decimal(round(sum(//(cac:InvoiceLine|cac:CreditNoteLine)/xs:decimal(cbc:LineExtensionAmount)) * 10 * 10) div 100))",
      "ruleset": "RO-CIUS-UBL-1.0.9"
    },
    {
      "severity": "FATAL",
      "stage": "BUSINESS_RULE",
      "ruleId": "BR-CO-13",
      "message": "[BR-CO-13]-Invoice total amount without VAT (BT-109) = Σ Invoice line net amount (BT-131) - Sum of allowances on document level (BT-107) + Sum of charges on document level (BT-108).",
      "location": "/*:Invoice[namespace-uri()='urn:oasis:names:specification:ubl:schema:xsd:Invoice-2'][1]/*:LegalMonetaryTotal[namespace-uri()='urn:oasis:names:specification:ubl:schema:xsd:CommonAggregateComponents-2'][1]",
      "test": "((cbc:ChargeTotalAmount) and (cbc:AllowanceTotalAmount) and (xs:decimal(cbc:TaxExclusiveAmount) = round((xs:decimal(cbc:LineExtensionAmount) + xs:decimal(cbc:ChargeTotalAmount) - xs:decimal(cbc:AllowanceTotalAmount)) * 10 * 10) div 100 )) or (not(cbc:ChargeTotalAmount) and (cbc:AllowanceTotalAmount) and (xs:decimal(cbc:TaxExclusiveAmount) = round((xs:decimal(cbc:LineExtensionAmount) - xs:decimal(cbc:AllowanceTotalAmount)) * 10 * 10 ) div 100)) or ((cbc:ChargeTotalAmount) and not(cbc:AllowanceTotalAmount) and (xs:decimal(cbc:TaxExclusiveAmount) = round((xs:decimal(cbc:LineExtensionAmount) + xs:decimal(cbc:ChargeTotalAmount)) * 10 * 10 ) div 100)) or (not(cbc:ChargeTotalAmount) and not(cbc:AllowanceTotalAmount) and (xs:decimal(cbc:TaxExclusiveAmount) = xs:decimal(cbc:LineExtensionAmount)))",
      "ruleset": "RO-CIUS-UBL-1.0.9"
    }
  ],
  "findingsTruncated": false,
  "previewCounts": {
    "fatal": 0,
    "error": 0,
    "warning": 0,
    "information": 0
  },
  "previewFindings": [],
  "previewFindingsTruncated": false,
  "sha256": "db8b2bc2b631db1e12416cbc4885bca3893e6f9c6066705a7284ef76cb348f86",
  "embeddedXmlSha256": null,
  "container": null,
  "checkedAt": "2026-07-29T11:24:49.650529Z",
  "reports": {},
  "error": null
}
```

</details>

<details>
<summary><strong>03. NOT_EVALUATED</strong> - unsupported CII syntax receives no technical decision</summary>

[`03_live_not_evaluated_output.json`](03_live_not_evaluated_output.json)

```json
{
  "inputIndex": 2,
  "documentId": "ro-unsupported-cii",
  "fileName": "unsupported_cii.xml",
  "processingStatus": "FAILED",
  "conformanceStatus": "NOT_EVALUATED",
  "previewConformanceStatus": "NOT_EVALUATED",
  "validationScope": "OFFLINE_PREFLIGHT",
  "externalStateStatus": "NOT_EVALUATED_EXTERNAL_STATE",
  "rulesetEffectiveAt": "2024-06-05",
  "sourceFormat": "UNKNOWN",
  "validationFamily": "UNKNOWN",
  "syntax": "UNKNOWN",
  "profile": "UNKNOWN",
  "scenario": null,
  "versions": {
    "ubl": "2.1",
    "ciusRo": "1.0.1",
    "roSchematron": "1.0.9",
    "embeddedEn16931": "1.3.8",
    "saxonHe": "10.9",
    "saxonHeSha256": "491d8edf4ec811d15c2b2417b007218b9b938f15e4dfbad004025beb4e70e960",
    "compiledSchematronSha256": "3088b39e24dab440dc98b55cb4ba6845a5fd22b382da1f376f592ee6e0d0f2eb",
    "temurinJreImage": "eclipse-temurin:21-jre-jammy@sha256:d63bd8d9b171999cbed8576f2c76e874dd4856791a358536e5c4d407e77edc13",
    "schematronSkeleton": "02f3707b194ce5792bf77b14a66d782c060abba3",
    "roRulesArchiveSha256": "818e7dd77e429f5dbde7c60b43dddbdf1a9a82a1773c359caa80a36ef89ea7f2",
    "ublArchiveSha256": "60b80d76394a8a2add90723ecb8e0e2e9d826775de9749df37a72d60703f86ed",
    "activeRuleset": {
      "name": "CIUS-RO 1.0.1 / ro16931-ubl 1.0.9",
      "effectiveAt": "2024-06-05"
    },
    "artifactManifestSha256": "39add0e63650bd7ee218eaeae8459ee912331280be57ee686815977dd7e404ce"
  },
  "counts": {
    "fatal": 0,
    "error": 0,
    "warning": 0,
    "information": 0
  },
  "findings": [],
  "findingsTruncated": false,
  "previewCounts": {
    "fatal": 0,
    "error": 0,
    "warning": 0,
    "information": 0
  },
  "previewFindings": [],
  "previewFindingsTruncated": false,
  "sha256": null,
  "embeddedXmlSha256": null,
  "container": null,
  "checkedAt": "2026-07-29T11:24:49.736973Z",
  "reports": {},
  "error": {
    "code": "UNSUPPORTED_DOCUMENT",
    "message": "The XML root does not match a supported invoice syntax"
  }
}
```

</details>

## Supported routes

- OASIS UBL 2.1 Invoice
- OASIS UBL 2.1 CreditNote
- CIUS-RO `1.0.1`
- Romanian Schematron package `ro16931-ubl 1.0.9`

CII and PDF are outside the current scope and return an explicit unsupported or `NOT_EVALUATED` result. Input can be supplied through HTTPS URL, inline XML, base64, console upload, or an Apify key-value store record.

## Machine-readable schema

Use [`dataset_record.schema.json`](dataset_record.schema.json) to validate stored rows before loading them into an ERP, webhook, Make, n8n, or another data pipeline.

```text
processingStatus -> SUCCEEDED | FAILED
conformanceStatus -> ACCEPTED | REJECTED | NOT_EVALUATED
validationScope -> OFFLINE_PREFLIGHT
externalStateStatus -> NOT_EVALUATED_EXTERNAL_STATE
findings[] -> severity, stage, ruleId, message, location
versions{} -> pinned rule and artifact identities
```

See [`DATA_NOTICE.md`](DATA_NOTICE.md) for run provenance, privacy boundaries, and interpretation limits.

## Release and integration

- Public Store availability: not released
- Verified private build: `0.0.4` `SUCCEEDED`
- Planned price: `$0.004` per evaluated invoice
- `NOT_EVALUATED` documents do not emit the `invoice-validated` event
- For release access or a custom ERP integration, contact the owner through the [Apify profile](https://apify.com/kamerozkan).

## License

The repository's original documentation, JSON samples, and schema are MIT licensed. Upstream rules, specifications, software, names, and marks retain their own licenses and terms.

## E-Invoice Automation Suite

This repository is part of a 16-product invoice automation family. Public Actor links are runnable Store listings. Private labels are release-state disclosures, not public availability claims.

- Public validators: [`xrechnung-xml-batch-validator-api`](https://apify.com/kamerozkan/xrechnung-xml-batch-validator-api) ([`xrechnung-xml-batch-validator-api-sample`](https://github.com/kamerozkan/xrechnung-xml-batch-validator-api-sample)), [`france-einvoice-validator`](https://apify.com/kamerozkan/france-einvoice-validator) ([`france-einvoice-validator-sample`](https://github.com/kamerozkan/france-einvoice-validator-sample)), [`italy-fatturapa-validator`](https://apify.com/kamerozkan/italy-fatturapa-validator) ([`italy-fatturapa-validator-sample`](https://github.com/kamerozkan/italy-fatturapa-validator-sample)), [`peppol-bis-preflight-validator`](https://apify.com/kamerozkan/peppol-bis-preflight-validator) ([`peppol-bis-preflight-validator-sample`](https://github.com/kamerozkan/peppol-bis-preflight-validator-sample)), and [`poland-ksef-preflight-validator`](https://apify.com/kamerozkan/poland-ksef-preflight-validator) ([`poland-ksef-preflight-validator-sample`](https://github.com/kamerozkan/poland-ksef-preflight-validator-sample)).
- Private validator preview: `romania-efactura-validator` ([`romania-efactura-validator-sample`](https://github.com/kamerozkan/romania-efactura-validator-sample)), private release preview with a successful hosted build.
- Private generators with successful hosted builds: `xrechnung-invoice-generator` ([`xrechnung-invoice-generator-sample`](https://github.com/kamerozkan/xrechnung-invoice-generator-sample)), `peppol-ubl-invoice-generator` ([`peppol-ubl-invoice-generator-sample`](https://github.com/kamerozkan/peppol-ubl-invoice-generator-sample)), `zugferd-facturx-pdf-generator` ([`zugferd-facturx-pdf-generator-sample`](https://github.com/kamerozkan/zugferd-facturx-pdf-generator-sample)), `fatturapa-invoice-generator` ([`fatturapa-invoice-generator-sample`](https://github.com/kamerozkan/fatturapa-invoice-generator-sample)), and `ksef-fa-invoice-generator` ([`ksef-fa-invoice-generator-sample`](https://github.com/kamerozkan/ksef-fa-invoice-generator-sample)).
- Parsers and converters: public [`zugferd-facturx-pdf-to-json`](https://apify.com/kamerozkan/zugferd-facturx-pdf-to-json) ([`zugferd-facturx-pdf-to-json-sample`](https://github.com/kamerozkan/zugferd-facturx-pdf-to-json-sample)); private release-ready `xrechnung-to-json-parser` ([`xrechnung-to-json-parser-sample`](https://github.com/kamerozkan/xrechnung-to-json-parser-sample)); private hosted-build-ready `peppol-ubl-to-json-parser` ([`peppol-ubl-to-json-parser-sample`](https://github.com/kamerozkan/peppol-ubl-to-json-parser-sample)), `zugferd-to-xrechnung-converter` ([`zugferd-to-xrechnung-converter-sample`](https://github.com/kamerozkan/zugferd-to-xrechnung-converter-sample)), and `ubl-cii-format-converter` ([`ubl-cii-format-converter-sample`](https://github.com/kamerozkan/ubl-cii-format-converter-sample)).
