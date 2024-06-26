# sj (Swagger Jacker)

sj is a command line tool designed to assist with auditing of exposed Swagger/OpenAPI definition files by checking the associated API endpoints for weak authentication. It also provides command templates for manual vulnerability testing.

It does this by parsing the definition file for paths, parameters, and accepted methods before using the results with one of three commands:
- `automate` - Crafts a series of requests and analyzes the status code of the response.
- `prepare` - Generates a list of commands to use for manual testing.
- `endpoints` - Generates a list of raw API routes. *Path values will not be replaced with test data*.
- `brute` - Sends a series of requests to a target to find operation definitions based on commonly used file paths.

## Build

To compile from source, ensure you have Go version `>= 1.20` installed and run `go build` from within the repository:

```bash
$ git clone https://github.com/BishopFox/sj.git
$ cd sj/
$ go build .
```

## Install

To install the latest version of the tool, run:

```bash
$ go install github.com/BishopFox/sj@latest
```

## Usage

> Use the `automate` command to send a series of requests to each defined endpoint and analyze the status code of each response.

![Automate Command](img/sj-automate.gif)

> Use the `prepare` command to prepare a list of curl commands for manual testing. You will likely have to modify these slightly.

![Prepare Command](img/sj-prepare.gif)

> Use the `endpoints` command to generate a list of raw endpoints from the provided definition file.

![Endpoints Command](img/sj-endpoints.gif)

> Use the `brute` command to send a series of requests in an attempt to find a definition file on the target.

```bash
$ sj brute -u https://<TARGET>
INFO[0000] Sending 2045 requests. This could take a while... 
INFO[0111] Found operation definitions embedded in JavaScript file at https://<TARGET>/example.js 
```

## Help

A full list of commands can be found by using the `--help` flag:

![Help Command](img/sj-help.gif)
