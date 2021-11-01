# http(s) requests

## Curl

Common used flags for `curl`:

* `[-b|--cookie]` - Read cookie data.
* `[-c|--cookie-jar <filename>]` - Write cookie data to this file.
* `[-d|--data]` - POST data using content-type _application/x-www-form-urlencoded_.
* `[-F|--form]` - POST data using content-type _multipart/form-data_.
* `[-H|--header]` - Extra header to include in the request.
* `[-i|--include]` - Print header in response.
* `[-X|--request]` - Request type to use.
* `[-L|--location]` - Follow server redirect.
* `[-O|--remote-name]` - Save to remote file name instead of piping to stdout.
* `[-S|--silent]` - Don't show progress or errors.

### Usage

Post login credentials and store authentication cookie in file, for usage in
subsequent requests:

    curl \
      --data "user=username" \
      --data "password=secret" \
      --cookie-jar ~/tmp/localhost:8080.session \
      "http://localhost:8080/login"

Post json-data, located in a file:

    curl \
      --header "Content-Type: application/json" \
      --data "@debug/device.json" \
      --cookie ~/tmp/localhost:8080.session \
      "http://localhost:8080/api/device/serial/0015"

Get json data:

    curl \
      --cookie ~/tmp/localhost:8080.session \
      --header "Accept: application/json" \
      "http://localhost:8080/api/device/serial/0015"

## Netcat

Netcat is available on almost all linux systems. It can be used for making simple
http requests in situations where it is not possible to install other packages.

### Usage

Example:

    nc -C www.google.com 80 << EOF
    GET / HTTP/1.1
    Host: www.google.com
    Connection: close

    EOF

## Openssl

`s_client` is a very useful diagnostic tool for SSL servers, see more @
`man s_client`.

### Usage

Example:

Check ssl certificate data with: `openssl s_client -connect <domain-name>:443`.
