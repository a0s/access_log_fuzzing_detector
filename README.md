# Access.log Fuzzing Detector
Very simple (and stupid) scanner that able to detect tries of [fuzzing](https://en.wikipedia.org/wiki/Fuzzing).

## Prerequisites

* ruby interpretator in PATH
* access.log should be in [default nginx format](https://nginx.org/en/docs/http/ngx_http_log_module.html)
* downloaded fuzzing dictionary (for example, you cat get it [here](https://github.com/Bo0oM/fuzz.txt/blob/master/fuzz.txt), 
[here](https://github.com/maurosoria/dirsearch/blob/master/db/dicc.txt), or [here](https://github.com/daviddias/node-dirbuster/tree/master/lists))

## Usage

Send access.log to stdin, and scanner will return you suspicious requests to stdout.

```sh
cat access.log | ruby scanner fuzz.txt
```
or
```sh
pv access.log | ruby scanner fuzz.txt
```
