# RFP Profile Gaps Discovered During Validation

These are **profile candidates**, not core specification gaps.

## Invoice profile candidates
- line discount and tax breakdown;
- payment terms;
- bank/payment destination;
- references to contract/work order/delivery/acceptance;
- issuer tax identity;
- invoice period/service period.

## Purchase-order profile candidates
- ordered/remaining amount semantics;
- line identifiers;
- goods/service classification;
- amendment/change-order references.

## Tax-document profile candidates
- jurisdiction-specific tax identifiers and validation;
- taxable base/rate/amount;
- linkage to commercial invoice.

## RFP business-context candidates
- payment category/type;
- vendor authoritative ID;
- procurement reference;
- tax applicability;
- contract requirement;
- amount/currency;
- organizational dimensions such as company/entity/cost center/business area where authoritative.

## Explicitly not core
- SAP-specific field names;
- a particular chart of accounts;
- customer-specific transaction types;
- customer-specific approval thresholds;
- local workflow role names;
- database table names;
- framework/controller/service/repository patterns.
