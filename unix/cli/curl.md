# curl

Make a POST request to a JSON endpoint using stdin as payload:

    echo "{}" | curl --json -d @- <url>

## Options

### HTTP request control

- `-X <method>` Use `method` HTTP method
- `-d <data>` Use `data` as HTTP payload (and use POST HTTP method unless a
  different one is specified with `-X`)
- `-d @-` Use stdin as HTTP payload
- `-d @<file>` Use contents of `file` as HTTP payload
- `--json <data>` Use `data` as payload, set `Content-Type` and `Accept` headers
  to `application/json`
- `-u <user>:<pass>` use HTTP basic authorization with supplied credentials

### Output control

- `-o <file>` direct output to file
- `-w <format>` write out specified response details to stdout
- `-s` disable progress bar and error messages (the progress bar is printed to
  stderr and active only when output is redirected to a file)
- `-f` fail with exit code 22 when HTTP response code is >= 400

#### `-w` format fields

- `%{response_code}` - HTTP response code
- `%{time_total}` - total time in seconds taken by the HTTP transaction
