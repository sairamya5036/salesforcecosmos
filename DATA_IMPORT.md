# Aether RMA Test Data Import

Import the seed data after deploying metadata.

The import is intentionally split into two phases because Salesforce requires
Standard Price Book entries before custom PricebookEntry records can be created,
and the Standard Price Book Id is org-specific.

## Commands

```bash
sf data import tree --plan aether_import_test_data.json --target-org YOUR_ORG_ALIAS
node scripts/data/create_standard_pricebook_entries.mjs YOUR_ORG_ALIAS
sf data import tree --plan aether_import_phase2_runtime.json --target-org YOUR_ORG_ALIAS
```

## Files

- `aether_import_test_data.json`: phase 1 plan for pricebook, products, accounts, contacts, assets, and service contract.
- `data/aether_import_test_data/*.json`: portable source seed records.
- `scripts/data/create_standard_pricebook_entries.mjs`: creates required Standard Price Book entries and generates phase 2 runtime files with target-org Ids.
- `aether_import_phase2_runtime.json` and `data/aether_import_runtime/`: generated locally and ignored by git.

Cases are linked to imported assets through `Case.AssetId`.
