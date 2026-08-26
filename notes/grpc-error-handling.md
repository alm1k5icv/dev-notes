# gRPC Error Handling

Prefer standard status codes from `google.golang.org/grpc/status`.

- Use `codes.Internal` for unexpected server errors.
- Use `codes.InvalidArgument` for client input problems.
- Attach details with `status.WithDetails()` for richer errors.
- Always log the full error server-side but return a sanitized message.

Example:

```go
st, _ := status.New(codes.Internal, "something broke").WithDetails(&errdetails.ErrorInfo{Reason: "DB down"})
return nil, st.Err()
```
