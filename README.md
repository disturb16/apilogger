# apilogger
Simple api logger for golang with the purpose of log basic information like api-key, clinet ip, request-id.

# Installation
Run `go get github.com/sanservices/apilogger`

# Usage

```go
ctx := context.Background()

// spects basic information in context: api-key, x-request-id, remote-address,
// second argument is the path to log file (if needed).
logger := apilogger.New(ctx, "")

logger.Info(LogCatDebug, "This is an info message")
logger.Warn(LogCatDebug, "This is a warning message")
logger.Error(LogCatDebug, "This is an error message")

logger.Infof(LogCatDebug, "This is an info message with %s", "some variable")
logger.Warnf(LogCatDebug, "This is a warning message with format, some number: %d", 100)
logger.Errorf(LogCatDebug, "This is an error message with format, %v", errors.New("An error"))

logger.InfoWF(LogCatDebug, &Fields{"message": "my message"})
logger.WarnWF(LogCatDebug, &Fields{"warning": "my warning", "other": "another message"})
logger.ErrorWF(LogCatDebug, &Fields{"error": errors.New("my error message")})
```

Outputs

```shell
INFO 2020/07/31 15:11:29 location="main.go:124", requestId="", clientIp="", apiKey="", sessionId="", ms="0.022536", function="apilogger.MyFunction", code="DBG01", type="debug", message="This is an info message"
WARNING 2020/07/31 15:11:29 location="main.go:125", requestId="", clientIp="", apiKey="", sessionId="", ms="0.107880", function="apilogger.MyFunction", code="DBG01", type="debug", message="This is a warning message"
ERROR 2020/07/31 15:11:29 location="main.go:126", requestId="", clientIp="", apiKey="", sessionId="", ms="0.141037", function="apilogger.MyFunction", code="DBG01", type="debug", message="This is an error message"

INFO 2020/07/31 15:11:29 location="main.go:128", requestId="", clientIp="", apiKey="", sessionId="", ms="0.161709", function="apilogger.MyFunction", code="DBG01", type="debug", message="This is an info message with some variable"
WARNING 2020/07/31 15:11:29 location="main.go:129", requestId="", clientIp="", apiKey="", sessionId="", ms="0.184334", function="apilogger.MyFunction", code="DBG01", type="debug", message="This is a warning message with format, some number: 100"
ERROR 2020/07/31 15:11:29 location="main.go:130", requestId="", clientIp="", apiKey="", sessionId="", ms="0.204437", function="apilogger.MyFunction", code="DBG01", type="debug", message="This is an error message with format, An error"

INFO 2020/07/31 15:11:29 location="main.go:132", requestId="", clientIp="", apiKey="", sessionId="", ms="0.227874", function="apilogger.MyFunction", code="DBG01", type="debug", message="my message"
WARNING 2020/07/31 15:11:29 location="main.go:133", requestId="", clientIp="", apiKey="", sessionId="", ms="0.251661", function="apilogger.MyFunction", code="DBG01", type="debug", other="another message", warning="my warning"
ERROR 2020/07/31 15:11:29 location="main.go:134", requestId="", clientIp="", apiKey="", sessionId="", ms="0.280195", function="apilogger.MyFunction", code="DBG01", type="debug", error="my error message"
```
