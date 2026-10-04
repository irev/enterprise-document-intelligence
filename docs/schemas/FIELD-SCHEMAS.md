# Field Schemas

Field schemas are versioned by document type. Define semantic meaning, type, cardinality, document-level requiredness, normalization and validation expectations.

## Invoice baseline
`invoice_number`, `invoice_date`, `due_date`, `vendor_name`, `vendor_identifier`, `purchase_order_number`, `currency`, `subtotal`, `tax_amount`, `total_amount`, `line_items`.

## Purchase Order baseline
`purchase_order_number`, `issue_date`, `supplier_name`, `supplier_identifier`, `currency`, `total_amount`, `line_items`, `validity`.

## Contract baseline
`contract_number`, `parties`, `effective_date`, `end_date`, `currency`, `contract_value`, `signatories`.

Do not mark a field document-required merely because one customer's workflow requires it. Document-schema requirements and business-process requirements are separate. Every material extracted field should support evidence and confidence.