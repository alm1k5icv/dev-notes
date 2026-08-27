# Structured Logging in Go

Date: 2026-08-27

Use `log/slog` for structured logs instead of ad hoc `fmt.Printf`.

## Key Points

- Use JSON handler in production, text handler in local dev.
- Include request ID, service, and error fields.
- Log at appropriate levels: Info for state changes, Error for failures, Debug for troubleshooting.
- Avoid logging sensitive data such as PII and tokens.

## Example

```go
slog.Info("request completed", "method", r.Method, "path", r.URL.Path, "duration_ms", ms)
```

## Follow-up

- Add a shared logging middleware for HTTP services.
- Standardize field names across services.