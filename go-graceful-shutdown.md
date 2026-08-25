# Graceful Shutdown in Go

When running HTTP servers in microservices, always shut down cleanly.

Use `http.Server` with a signal handler:

```go
srv := &http.Server{Addr: ":8080"}
go srv.ListenAndServe()

stop := make(chan os.Signal, 1)
signal.Notify(stop, syscall.SIGINT, syscall.SIGTERM)
<-stop

ctx, cancel := context.WithTimeout(context.Background(), 5*time.Second)
defer cancel()
if err := srv.Shutdown(ctx); err != nil {
    log.Fatal(err)
}
```

This lets in-flight requests finish before exiting. Add this to your service startup for smoother deployments.
