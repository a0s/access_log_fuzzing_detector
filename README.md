# Access.log Fuzzing Detector
Very simple (and stupid) scanner that able to detect tries of [fuzzing](https://en.wikipedia.org/wiki/Fuzzing).

## Prerequisites

* ruby interpretator in PATH
* access.log should be in [default nginx format](https://nginx.org/en/docs/http/ngx_http_log_module.html)
* downloaded fuzzing dictionary (for example, you cat get it [here](https://github.com/Bo0oM/fuzz.txt/blob/master/fuzz.txt), 
[here](https://github.com/maurosoria/dirsearch/blob/master/db/dicc.txt), or [here](https://github.com/daviddias/node-dirbuster/tree/master/lists))

## Usage

Send access.log to stdin, and scanner will return you suspicious requests to stdout. Use `cat`

```sh
cat access.log | ruby scanner fuzz.txt
```
or `pv` if you want to see overall progress/speed
```sh
pv access.log | ruby scanner fuzz.txt
```
## How it works
Every input line in stdin will process by stages:
1) Parse request with [regular expression](https://github.com/a0s/access_log_fuzzing_detector/commit/ebea2fad1cdc062aa770123098fd044d47f7de1b#diff-bbdaea376f500d25f6b0c1050311dd07R26). In case of failure it returns `RegexpSucks` exception :)
2) Check `method` of request. Allowed methods are `GET HEAD POST PUT DELETE CONNECT OPTIONS TRACE PATCH`
3) Check `protocol` of request. Allower protocols are `HTTP/1.0 HTTP/1.1`
4) For every `line/from/dictionary` we will check:
   * `request_uri` not start with `line/from/dictionary`
   * `request_uri` not start with `/line/from/dictionary`
   * `request_uri` not end with `line/from/dictionary`
