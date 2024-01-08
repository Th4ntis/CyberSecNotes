# GoBuster

[GoBuster](https://github.com/OJ/gobuster) is a tool used to brute-force:

* URIs (directories and files) in web sites.
* DNS subdomains (with wildcard support).
* Virtual Host names on target web servers.
* Open Amazon S3 buckets

## Installing GoBuster

#### Using go install

If you have a Go environment ready to go (at least go 1.16), it's as easy as: `go install github.com/OJ/gobuster/v3@latest`

#### Building From Source

Since this tool is written in [Go](https://go.dev/) you need to install the Go language/compiler/etc. Full details of [installation](https://golang.org/doc/install) and set up can be found on the Go language website. Once installed you have two options. You need at least go 1.16.0 to compile gobuster.

Compiling gobuster has external dependencies, and so they need to be pulled in first:

`go get && go build` This will create a gobuster binary for you. If you want to install it in the $GOPATH/bin folder you can run:

`go install` If you have all the dependencies already, you can make use of the build scripts:

* `make` - builds for the current Go configuration (ie. runs go build).
* `make windows` - builds 32 and 64 bit binaries for windows, and writes them to the build folder.
* `make linux` - builds 32 and 64 bit binaries for linux, and writes them to the build folder.
* `make darwin` - builds 32 and 64 bit binaries for darwin, and writes them to the build folder.
* `make all` - builds for all platforms and architectures, and writes the resulting binaries to the build folder.
* `make clean` - clears out the build folder.
* `make test` - runs the tests.

## Modes

#### DNS Mode

```
Usage:
  gobuster dns [flags]

Flags:
  -d, --domain string      The target domain
  -h, --help               help for dns
  -r, --resolver string    Use custom DNS server (format server.com or server.com:port)
  -c, --show-cname         Show CNAME records (cannot be used with '-i' option)
  -i, --show-ips           Show IP addresses
      --timeout duration   DNS resolver timeout (default 1s)
      --wildcard           Force continued operation when wildcard found

Global Flags:
  -z, --no-progress       Don't display progress
  -o, --output string     Output file to write results to (defaults to stdout)
  -q, --quiet             Don't print the banner and other noise
  -t, --threads int       Number of concurrent threads (default 10)
      --delay duration    Time each thread waits between requests (e.g. 1500ms)
  -v, --verbose           Verbose output (errors)
  -w, --wordlist string   Path to the wordlist
```

#### DIR Mode

```
Usage:
gobuster dir [flags]

Flags:
-f, --add-slash                     Append / to each request
-c, --cookies string                Cookies to use for the requests
-e, --expanded                      Expanded mode, print full URLs
-x, --extensions string             File extension(s) to search for
-r, --follow-redirect               Follow redirects
-H, --headers stringArray           Specify HTTP headers, -H 'Header1: val1' -H 'Header2: val2'
-h, --help                          help for dir
-l, --include-length                Include the length of the body in the output
-k, --no-tls-validation             Skip TLS certificate verification
-n, --no-status                     Don't print status codes
-P, --password string               Password for Basic Auth
-p, --proxy string                  Proxy to use for requests [http(s)://host:port]
-s, --status-codes string           Positive status codes (will be overwritten with status-codes-blacklist if set) (default "200,204,301,302,307,401,403")
-b, --status-codes-blacklist string Negative status codes (will override status-codes if set)
    --timeout duration              HTTP Timeout (default 10s)
-u, --url string                    The target URL
-a, --useragent string              Set the User-Agent string (default "gobuster/3.1.0")
-U, --username string               Username for Basic Auth
-d, --discover-backup               Upon finding a file search for backup files
    --wildcard                      Force continued operation when wildcard found

Global Flags:
-z, --no-progress       Don't display progress
-o, --output string     Output file to write results to (defaults to stdout)
-q, --quiet             Don't print the banner and other noise
-t, --threads int       Number of concurrent threads (default 10)
    --delay duration    Time each thread waits between requests (e.g. 1500ms)
-v, --verbose           Verbose output (errors)
-w, --wordlist string   Path to the wordlist
```

#### VHost Mode

```
Usage:
gobuster vhost [flags]

Flags:
-c, --cookies string        Cookies to use for the requests
-r, --follow-redirect       Follow redirects
-H, --headers stringArray   Specify HTTP headers, -H 'Header1: val1' -H 'Header2: val2'
-h, --help                  help for vhost
-k, --no-tls-validation     Skip TLS certificate verification
-P, --password string       Password for Basic Auth
-p, --proxy string          Proxy to use for requests [http(s)://host:port]
    --timeout duration      HTTP Timeout (default 10s)
-u, --url string            The target URL
-a, --useragent string      Set the User-Agent string (default "gobuster/3.1.0")
-U, --username string       Username for Basic Auth

Global Flags:
-z, --no-progress       Don't display progress
-o, --output string     Output file to write results to (defaults to stdout)
-q, --quiet             Don't print the banner and other noise
-t, --threads int       Number of concurrent threads (default 10)
    --delay duration    Time each thread waits between requests (e.g. 1500ms)
-v, --verbose           Verbose output (errors)
-w, --wordlist string   Path to the wordlist
```

## Usage

gobuster -w (wordlist) -u (url)

Example: `gobuster -w /opt/SecLists/Discovery/Web-Content/directory-list-lowercase-2.3-small.txt -u https://192.168.1.60`

![](<../../.gitbook/assets/image (529).png>)
