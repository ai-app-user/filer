# Filer Development Guidelines

Filer follows the shared WSync architecture:

- Use `dev` as the default branch.
- Push completed iteration commits to `dev`.
- Merge or push to `main` only when explicitly requested.
- Keep jobs independent and connected only by queues.
- Name jobs by role and show backend identity as a suffix in pipeline output:
  `[MetaReader-NFS-8]`, `[DataReader-NFS-112]`, `[DataWriter-NFS-64]`.
- Keep product scenarios and command behavior in Hypersync.
- Keep reusable pipeline infrastructure in Piper.
- Keep filesystem/backend I/O mechanics in Filer.

## Pipeline Vocabulary

- `[JobName-N/options]`: concrete job instance.
- `(QueueName-N/options)`: concrete queue or queue family.
- `{PipelineName}`: reusable pipeline block.
- `{{ScenarioName}}`: product or benchmark scenario owned by a consuming app.

Filer may define `{MetaReader}`, `{DataReader}`, and `{DataWriter}` pipeline
blocks, but full scenarios such as `{{Scanner}}` or `{{Copy}}` belong in
Hypersync.
