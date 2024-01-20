# Go Logger interface – zap implementation

This library provides an implementation of the [Logger interface](https://github.com/secondtruth/go-logger)
for [zap](https://github.com/uber-go/zap).

## Installation

To install `go-logger-zap`, use the following command:

	go get -u github.com/secondtruth/go-logger-zap

## Quick Start

```go
package main

import (
	"os"

	zaplogger "github.com/secondtruth/go-logger-zap/logger"
	"github.com/secondtruth/go-logger/logger"
	"go.uber.org/zap"
	"go.uber.org/zap/zapcore"
)

func main() {
	consoleEncoder := zapcore.NewJSONEncoder(zap.NewDevelopmentEncoderConfig())
	core := zapcore.NewCore(consoleEncoder,
		zapcore.Lock(zapcore.AddSync(os.Stderr)),
		zapcore.DebugLevel)
	zapLog := zap.New(core)
	log, _ := zaplogger.NewZapLogger(zapLog)

 	log.WithFields(logger.Fields{
		"foo": "bar",
	}).Info("message")
}
```
