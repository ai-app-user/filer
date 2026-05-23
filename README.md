# Filer

Filer owns filesystem-facing jobs and backend adapters used by Hypersync.

The project boundary is intentionally narrower than Hypersync:

- metadata readers for filesystem-like sources
- data readers for filesystem-like sources
- target metadata/data writers for filesystem-like targets
- NFS and NULL backend adapters

Filer does not own product scenarios, profiling policy, diff policy, copy/sync
commands, user-facing UX, or performance gates. Those stay in Hypersync.

Current consumers still include Filer through the shared workspace build:

```text
piper/src -> utils/src -> connector/src -> filer/src -> hypersync/src
```

The C++ namespace remains `hypersync` during this extraction phase so the move
is mechanical and low-risk. Namespace cleanup can happen later after the project
boundary has settled.
