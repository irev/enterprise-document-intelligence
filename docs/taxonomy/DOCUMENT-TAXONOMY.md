# Document Taxonomy

Taxonomy defines **what a document is**, not which workflow uses it. Business context is separate. Keep hierarchy shallow and annotation-consistent. UNKNOWN is mandatory.

```text
FINANCIAL
  INVOICE: COMMERCIAL_INVOICE, PROFORMA_INVOICE, CREDIT_NOTE
  TAX_DOCUMENT: TAX_INVOICE, WITHHOLDING_TAX, TAX_PAYMENT_RECEIPT
  PAYMENT_PROOF
PROCUREMENT
  PURCHASE_REQUEST, PURCHASE_ORDER, QUOTATION, CONTRACT, WORK_ORDER
FULFILLMENT
  DELIVERY_ORDER, GOODS_RECEIPT, SERVICE_ACCEPTANCE, COMPLETION_REPORT
CORPORATE
  MEMO, LETTER, APPROVAL, MINUTES
BANKING
  BANK_STATEMENT, TRANSFER_RECEIPT, BANK_CONFIRMATION
IDENTITY
  COMPANY_IDENTITY, TAX_IDENTITY, BANK_ACCOUNT_INFORMATION
OTHER
  UNKNOWN
```

Example business context:
```json
{"business_domain":"ACCOUNTS_PAYABLE","process":"REQUEST_FOR_PAYMENT"}
```

Do not create workflow-coupled types such as `RFP_INVOICE` when the underlying document is an invoice. New classes require definitions, examples, exclusions and evaluation coverage.