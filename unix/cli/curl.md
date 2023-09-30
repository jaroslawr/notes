# curl

Send HTTP POST request with stdin as request payload, stripping CR/LF from the
input:

    curl --data @- <url>

Send HTTP POST request with stdin as request payload, without input
postprocessing:

    curl --data-binary @- <url>

Show HTTP statistics regarding timing etc., as JSON:

    curl -w '%{json}' -o /dev/null <url>

Write a HTTP log file with request headers, response headers and response body:

    curl -vsS <url> &>log

## Notes

1. Use of stdout and stderr by curl is a complicated story:
    - response body is written to stdout
    - output enabled by `-v/--verbose` is written to stderr
    - output enabled by `-w/--write-out` is written to stdout after the response
      body
    - `-o/--output <file>` makes curl write the response body to `file` and
      optionally also the response headers if `-i/--include` is enabled, but it
      does not affect the output that is enabled by `-v/--verbose` or by
      `-w/--write-out`
    - when stdout is not a tty curl starts printing a progress bar on stderr,
      even when stderr itself is also redirected
    - progress bar can be disabled with `-s/--silent`, but this also disables
      error reporting, which can be reenabled with `-S/--show-error`

2. `--data <data>` does postprocessing on the data, removing carriage returns
   and newlines, so it is necessary to use `--data-binary <data>` to send data
   exactly as given.

## Options

### HTTP request control

| Short option | Long option            | Description
| ------------ | ---------------------- | -----------
| `-X`         | `--request <method>`   | Use `method` HTTP method
| `-H`         | `--header <header>`    | Send `header` as part of the HTTP request
| `-d`         | `--data <data>`        | Send `data` as HTTP payload, stripping CR/LF
| `-d`         | `--data @-`            | Send stdin as HTTP payload, stripping CR/LF
| `-d`         | `--data @<file>`       | Send contents of `file` as HTTP payload, stripping CR/LF
|              | `--json <data>`        | Send `data` as HTTP JSON payload, stripping CR/LF
|              | `--data-binary <data>` | Send `data` as HTTP payload, exactly as given
| `-u`         | `--user <user>:<pass>` | Use HTTP basic authorization with supplied credentials

### Output control

| Short option  | Long option                   | Description
| ------------- | ----------------------------- | -----------
| `-o`          | `--output <file>`             | Write output (response body) to `file`
| `-i`          | `--include`                   | Include response headers in output
| `-w`          | `--write-out <format-string>` | Write out statistics given by `format-string` to stdout
| `-s`          | `--silent`                    | Disable progress bar and error messages 
| `-S`          | `--show-error`                | Enable error messages (when disabled with `--silent`)
| `-f`          | `--fail`                      | Fail with exit code 22 when HTTP response code is >= 400

### Format string syntax for `--write-out`

| Variable           | Description
| ------------------ | -------
| `%{response_code}` | HTTP response code
| `%{time_total}`    | Total time in seconds taken by the HTTP transaction
