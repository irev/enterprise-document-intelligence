# Canonical Document Schema

The canonical schema is the production exchange contract. It is neither a training-row format nor a model prompt.

```json
{
  "document_id":"doc_01...",
  "schema_version":"1.0",
  "source":{"filename":"invoice.pdf","mime_type":"application/pdf","sha256":"...","size_bytes":183829,"page_count":2},
  "context":{"tenant_id":"tenant_001","business_domain":"ACCOUNTS_PAYABLE","process":"REQUEST_FOR_PAYMENT"},
  "classification":{"family":"FINANCIAL","type":"INVOICE","subtype":"COMMERCIAL_INVOICE","confidence":0.982,"model_version":"classifier-2.1"},
  "entities":{},
  "quality":{},
  "validation":{"status":"REVIEW_REQUIRED","findings":[]},
  "provenance":{},
  "review":{},
  "audit":{}
}
```

## Field contract
```json
{
  "invoice_number":{
    "raw_value":"INV-001",
    "normalized_value":"INV-001",
    "confidence":0.984,
    "evidence":[{"page":1,"text":"Invoice No: INV-001","bounding_box":[0.62,0.11,0.83,0.15]}],
    "extractor":{"model":"document-extractor","version":"1.3"}
  }
}
```

Define bounding-box coordinate conventions explicitly. Preserve raw values for evidence/audit and normalized values for machine processing. Monetary values require decimal-safe representation and explicit currency.