# Filer Design

Filer is the reusable filesystem I/O layer for WSync projects.

## Scope

Filer owns jobs and adapters that directly read from or write to filesystem-like
backends:

- `{MetaReader}` backend implementations for NFS and future local filesystem
  backends
- `{DataReader}` backend implementations for NFS and synthetic/file-backed
  payload sources where they are used as filesystem readers
- `{DataWriter}` backend implementations for NFS and NULL targets
- target metadata writers such as directory creation and metadata restoration
- backend connection/session management, endpoint expansion, health checks, and
  target writer lifecycle state

Filer does not own product scenarios. A scenario such as `{{Scanner}}`,
`{{Generator}}`, `{{Copy}}`, or `{{Sync}}` belongs to Hypersync, which composes
Filer jobs with Piper queues and Hypersync-specific policy.

## Notation

Filer follows the same composition vocabulary as Piper and Hypersync:

- `[JobName-N/options]` is a concrete job instance.
- `(QueueName-N/options)` is a concrete queue or queue family.
- `{PipelineName}` is a reusable pipeline block with declared inputs, outputs,
  configuration, and variations.
- `{{ScenarioName}}` is a product or benchmark scenario owned by the consuming
  application.

Filer should document jobs and reusable pipeline blocks, but avoid defining
product scenarios except as examples.

## Current Extraction Boundary

The first extraction keeps shared record schemas, codecs, product commands,
profiler logic, and scenario registry in Hypersync. Filer currently contains:

- `core/nfs_backend.*`
- `jobs/data_writer/*`
- `jobs/nfs_data_reader/*`
- `jobs/nfs_meta_reader/*`

This keeps the move small enough to validate without changing behavior. The
next boundary cleanup can move generic file schemas or backend-independent file
interfaces only after the performance gates are stable.
