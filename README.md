> **Live API:** [Run Romania e-Factura Validator on Apify](https://apify.com/kamerozkan/romania-efactura-validator)

# Romania e-Factura Validator API: Samples and JSON Schema

[![Apify Actor](https://img.shields.io/badge/Apify-Run%20Actor-00c7b7?logo=apify)](https://apify.com/kamerozkan/romania-efactura-validator)
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

## Real output examples

All three records below are verbatim rows from successful run `FVLTBJAZyNfTn2epm`, dataset `JAkABPptE7mBiYAng`.

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
    "schematronSkeleton": "02f3707b194ce5792bf77b14a66d782c060abba3",
    "roRulesArchiveSha256": "818e7dd77e429f5dbde7c60b43dddbdf1a9a82a1773c359caa80a36ef89ea7f2",
    "ublArchiveSha256": "60b80d76394a8a2add90723ecb8e0e2e9d826775de9749df37a72d60703f86ed",
    "activeRuleset": {
      "name": "CIUS-RO 1.0.1 / ro16931-ubl 1.0.9",
      "effectiveAt": "2024-06-05"
    },
    "artifactManifestSha256": "289298a3e037eb1fb073761391d9503f771dfa0ae5edd8372a912b477d4891aa"
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
  "checkedAt": "2026-07-29T10:39:19.574825Z",
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
    "schematronSkeleton": "02f3707b194ce5792bf77b14a66d782c060abba3",
    "roRulesArchiveSha256": "818e7dd77e429f5dbde7c60b43dddbdf1a9a82a1773c359caa80a36ef89ea7f2",
    "ublArchiveSha256": "60b80d76394a8a2add90723ecb8e0e2e9d826775de9749df37a72d60703f86ed",
    "activeRuleset": {
      "name": "CIUS-RO 1.0.1 / ro16931-ubl 1.0.9",
      "effectiveAt": "2024-06-05"
    },
    "artifactManifestSha256": "289298a3e037eb1fb073761391d9503f771dfa0ae5edd8372a912b477d4891aa"
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
  "checkedAt": "2026-07-29T10:39:21.106612Z",
  "reports": {},
  "error": null
}
```

</details>

<details>
<summary><strong>03. NOT_EVALUATED</strong> - unsafe source rejected before validation</summary>

[`03_live_not_evaluated_output.json`](03_live_not_evaluated_output.json)

```json
{
  "inputIndex": 2,
  "documentId": "ro-not-evaluated",
  "fileName": "http-source.xml",
  "processingStatus": "FAILED",
  "conformanceStatus": "NOT_EVALUATED",
  "previewConformanceStatus": "NOT_EVALUATED",
  "validationScope": "OFFLINE_PREFLIGHT",
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
    "schematronSkeleton": "02f3707b194ce5792bf77b14a66d782c060abba3",
    "roRulesArchiveSha256": "818e7dd77e429f5dbde7c60b43dddbdf1a9a82a1773c359caa80a36ef89ea7f2",
    "ublArchiveSha256": "60b80d76394a8a2add90723ecb8e0e2e9d826775de9749df37a72d60703f86ed",
    "activeRuleset": {
      "name": "CIUS-RO 1.0.1 / ro16931-ubl 1.0.9",
      "effectiveAt": "2024-06-05"
    },
    "artifactManifestSha256": "289298a3e037eb1fb073761391d9503f771dfa0ae5edd8372a912b477d4891aa"
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
  "checkedAt": "2026-07-29T10:39:21.171757Z",
  "reports": {},
  "error": {
    "code": "SOURCE_FETCH_FAILED",
    "message": "Only HTTPS source URLs are allowed"
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
findings[] -> severity, stage, ruleId, message, location
versions{} -> pinned rule and artifact identities
```

See [`DATA_NOTICE.md`](DATA_NOTICE.md) for run provenance, privacy boundaries, and interpretation limits.

## Use the live API

- [Run the Actor on Apify](https://apify.com/kamerozkan/romania-efactura-validator)
- Price: `$0.004` per evaluated invoice
- `NOT_EVALUATED` documents do not emit the `invoice-validated` event

## License

The repository's original documentation, JSON samples, and schema are MIT licensed. Upstream rules, specifications, software, names, and marks retain their own licenses and terms.
