# Logaro

![build](https://github.com/goify/logaro/workflows/build/badge.svg)
![license](https://img.shields.io/github/license/goify/logaro?color=success)
![Go version](https://img.shields.io/github/go-mod/go-version/goify/logaro)
[![GoDoc](https://godoc.org/github.com/goify/logaro?status.svg)](https://godoc.org/github.com/goify/logaro)

`Logaro` is a lightweight Go package for JSON-based logging. It provides a simple and flexible logging solution with support for log levels, log entry customization, and hierarchical loggers.

## Features

- JSON-based logging format for easy log consumption and analysis.
- Configurable log levels to control the verbosity of the log output.
- Ability to customize log entries with additional fields.
- Hierarchical loggers to organize and inherit log settings.
- Support for serializers to transform log message and field values.

## Installation

To use Logaro in your Go project, you need to have Go installed and set up. Then, run the following command to install the package:

```bash
go get github.com/goify/logaro
```

## Usage

Here's a basic example of how to use Logaro:

```go
package main

import "github.com/goify/logaro"


func main() {
 // Create a logger
 logger := logaro.GenerateLogger()

 // Log a message
 logger.Log("info", "Hello, Logaro!", nil)

 // Log a message with additional fields
 logger.Log("error", "An error occurred", map[string]interface{}{
  "error_code": 500,
  "error_msg":  "Internal Server Error",
 })

 // Create a child logger with additional fields
 childLogger := logger.WithFields(map[string]interface{}{
  "component": "subsystemA",
 })

 // Log from the child logger
 childLogger.Log("debug", "Debug message from subsystemA", nil)
}
```

For more detailed examples and advanced usage, please refer to the [examples](/examples) directory.

## Output

Using Logaro, the log entries can be output in a JSON format. Here's an example of how the log entries would appear when logged to the standard output:

```json
{"timestamp":"2023-05-10T10:30:45Z","message":"This is an informational message","level":"info","fields":null}
{"timestamp":"2023-05-10T10:30:45Z","message":"This is a warning message","level":"warn","fields":null}
{"timestamp":"2023-05-10T10:30:45Z","message":"This is an error message","level":"error","fields":null}
{"timestamp":"2023-05-10T10:30:45Z","message":"Debugging information","level":"debug","fields":{"user_id":123,"request_id":"abc123"}}
{"timestamp":"2023-05-10T10:30:45Z","message":"Child logger message","level":"info","fields":{"component":"subsystemA"}}
{"timestamp":"2023-05-10T10:30:45Z","message":"Custom serialization example","level":"info","fields":{"field":"Value"}}
```

The log entries are represented as JSON objects, where each object contains the `timestamp`, `message`, `level`, and `fields` properties. The `fields` property contains additional key-value pairs associated with the log entry.

Please note that the actual log output may vary based on the specific log messages, log levels, and fields provided in your application.

Feel free to customize and expand upon this output example section based on your specific package functionality and desired log format.

## API

### `type Logger`

Represents a logger instance that can be used to log messages at different levels.

#### Methods

- `Log(level string, message string, fields map[string]interface{})`
  Logs a message at the specified log `level`. Additional `fields` can be provided as a map of key-value pairs.

- `Child(fields map[string]interface{}) *Logger`
  Creates a child logger with the specified additional `fields`. The child logger inherits the log settings and fields from its parent.
  ssss
- `WithFields(fields map[string]interface{}) *Logger`
  Creates a child logger with the specified additional `fields`. The child logger inherits the log settings and fields from its parent.

- `WithSerializers(serializers map[string]func(interface{}) interface{}) *Logger`
  Creates a child logger with custom `serializers` for transforming log message and field values. The serializers argument should be a map where the keys represent the fields to be serialized and the values are functions that perform the serialization.

### `type LogEntry`

Represents a log entry containing the log message, log level, and additional fields.

#### Fields

- `Timestamp string`
  The timestamp of the log entry in RFC3339 format.

- `Message string`
  The log message.

- `Level string`
  The log level.

- `Fields map[string]interface{}`
  Additional fields associated with the log entry.

### `func NewLogger() *Logger`

Creates a new instance of the `Logger` with default settings.

This API section provides an overview of the available types, methods, and functions in the Logaro package. Please refer to the code documentation and examples for more details on how to use the API effectively.

Feel free to customize and expand upon this API section based on your specific package functionality and features.

## Documentation

For detailed documentation and API reference, please refer to the [GoDoc](https://godoc.org/github.com/goify/logaro) page.

## Support

Logaro is an MIT-licensed open source project. It can grow thanks to the sponsors and support.

## License

Logaro is [MIT licensed](LICENSE).
