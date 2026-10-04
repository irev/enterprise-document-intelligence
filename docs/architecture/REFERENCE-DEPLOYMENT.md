# Reference Deployment Architecture

This is a logical reference, not a mandatory technology stack.

```text
                    +------------------+
Client / RFP ------>| API Gateway/Auth |
                    +--------+---------+
                             |
                             v
                    +------------------+
                    | Ingestion API    |
                    +----+--------+----+
                         |        |
                    object/data   +----> event/queue
                      storage              |
                                           v
                                  +------------------+
                                  | Orchestrator     |
                                  +--+--+--+--+------+
                                     |  |  |  |
                         +-----------+  |  |  +----------+
                         v              v  v             v
                      Parser/OCR   Classifier       Extractor
                                      |                |
                                      +-------+--------+
                                              v
                                      Validation Engine
                                              |
                              +---------------+---------------+
                              v                               v
                        Review Service                  Result Store
                              |                               |
                              +---------------+---------------+
                                              v
                                      API / Events to RFP
```

## Deployment properties

- stateless compute where practical;
- durable source/result storage;
- queue-backed asynchronous work for expensive stages;
- tenant-scoped authorization at every data access boundary;
- isolated/sandboxed processing for untrusted documents;
- independent scaling of OCR/model workers;
- immutable/versioned model and configuration artifacts;
- centralized secrets management;
- structured logs, metrics and traces without document-content leakage.

## Model serving

Model workers are replaceable adapters. Local models, managed APIs, specialized OCR, classifiers and VLMs may coexist. The canonical result contract prevents provider details from leaking to consumers.

## Failure isolation

A parser/model failure must not corrupt authoritative business data. Dead-letter/quarantine behavior, bounded retries, timeout budgets and explicit failure states are required implementation concerns.

## Environment separation

Development/test/staging/production use separate credentials, storage and governed datasets. Production documents must not flow into lower environments by default.