# Indian Payment SMS Corpus

A privacy-safe, redacted parser corpus for Indian bank, UPI, wallet, ATM, transfer, and card-payment SMS.

## At a glance

| Measure | Value |
| --- | ---: |
| Total rows | 172 |
| Seed fixtures | 58 |
| Numeric variants | 114 |
| Completed debits | 78 |
| Credits and refunds | 21 |
| Reversals | 6 |
| Hard negatives and future events | 67 |

The corpus is designed for parser development, classification, regression tests, and safety evaluation. It is not a spending survey and should not be treated as a statistical sample of Indian consumers.

## Data status

Most rows are synthetic variants grounded in genuine public OSS examples, test fixtures, and documented parser edge cases. Every SMS body in this repository is a synthetic, redacted rewrite. No row is claimed to be a verified real-user SMS, and no private inbox data is included.

Rows with `variant_of` preserve a seed message's grammar while changing monetary values and numeric identifiers. They are augmentation data, not additional real-world observations.

The corpus includes positive and negative cases for:

- UPI, card, bank-account, ATM, transfer, and wallet messages
- debits, credits, refunds, reversals, card bills, mandates, and upcoming debits
- balances, limits, OTPs, promotions, failed or declined payments, personal messages, and phishing-like alerts

## Repository layout

```text
data/indian-payment-sms-dataset.json   Dataset and expected parser labels
SOURCES.md                             Provenance and license ledger
LICENSE                                CC BY 4.0 notice for authored synthetic data
CITATION.cff                           Citation metadata
```

## Record shape

Each row contains a stable `id`, `source_ids`, provenance metadata, a synthetic `raw_sms` body, and an `expected` object. Monetary values are stored as integer paise:

```json
{
  "id": "upi-hdfc-multiline-001",
  "kind": "debit",
  "rail": "upi",
  "raw_sms": "Sent Rs.500.00 from HDFC Bank A/C XX1234...",
  "expected": {
    "bookable": true,
    "direction": "debit",
    "currency": "INR",
    "transaction_amount_paise": 50000
  }
}
```

Use `expected.bookable` as the safety label. Amounts in balances, limits, bills, OTP prompts, failed payments, and future debits must not become new expenses.

## Provenance and credits

The complete source ledger is in [SOURCES.md](SOURCES.md). Each row carries `source_ids` that point to the grammar or edge case that informed it. Sources with unclear redistribution rights were reviewed for discovery and credited where appropriate, but their text was not copied.

The corpus includes independently authored rewrites informed by licensed OSS projects under MIT, AGPL-3.0, and GPL-3.0. Third-party projects remain under their own licenses; this repository does not relicense their source code or text.

## License

The SplitEasy-authored synthetic dataset and documentation in this repository are available under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Please credit **SplitEasy contributors, Indian Payment SMS Corpus**, and link to this repository.

This license does not grant rights to third-party source code, names, trademarks, or any material copied directly from an upstream project. See [SOURCES.md](SOURCES.md) for attribution and upstream license details.

## Privacy and contributions

Do not contribute a real SMS unless you have permission to share it. Redact names, phone numbers, account and card numbers, UPI IDs, references, URLs, order IDs, and support numbers. Keep only the grammar needed for parser coverage, update [SOURCES.md](SOURCES.md), and add expected labels for every new row.
