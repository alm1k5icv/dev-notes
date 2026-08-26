# Graceful Shutdown in Go Microservices

- Use `http.Server.Shutdown(ctx)` instead of manually closing listeners.
- Keep a root context for the whole app and cancel it on SIGTERM/SIGINT.
- Wait for in-flight requests with a timeout; 10s is usually enough for internal APIs.
- For gRPC, use `grpcServer.GracefulStop()`; only fall back to `Stop()` if the deadline is exceeded.
- Drain message consumers before exiting, especially with Kafka/RabbitMQ.
- Log shutdown stages clearly so debugging production restarts is easier.

Example flow:
1. Listen for signals
2. Stop accepting new work
3. Shut down HTTP/gRPC servers
4. Close clients/db connections
5. Exit with code 0 or non-zero on failure