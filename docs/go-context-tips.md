# Go Context Tips

- Always pass `context.Context` as the first argument to functions that do I/O.
- Use `context.WithTimeout` for HTTP clients and DB calls; set sensible defaults.
- Don't store contexts in structs; pass them explicitly.
- Check `ctx.Err()` after long-running operations to respect cancellation.
- For microservices, propagate `traceID` via context values, not globals.

_Added 2026-08-14._