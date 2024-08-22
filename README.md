# Go Zabbix API

Note, this is not tested and is adjusted for use of tpretz/terraform-provider-zabbix

[![GoDoc](https://godoc.org/github.com/tpretz/go-zabbix-api?status.svg)](https://godoc.org/github.com/tpretz/go-zabbix-api) [![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE) [![Build Status](https://travis-ci.org/tpretz/go-zabbix-api.svg?branch=master)](https://travis-ci.org/tpretz/go-zabbix-api)

This Go package provides access to the Zabbix API. Due to dependencies, the
minimum version required is 1.21.

Tested on Zabbix 6.0 and 7.0.

https://www.zabbix.com/documentation/6.0/en/manual/api
https://www.zabbix.com/documentation/7.0/en/manual/api

This package aims to provide a full-featured Go module for the Zabbix API.

## Install

Install it: `go get github.com/tpretz/go-zabbix-api`

## Getting started

```go
package main

import (
        "fmt"

        "github.com/tpretz/go-zabbix-api"
)

func main() {
        user := "MyZabbixUsername"
        pass := "MyZabbixPassword"
        var config zabbix.Config
        config.Url = "http://localhost/api_jsonrpc.php"

        api := zabbix.NewAPI(config)
        api.Login(user, pass)

        res, err := api.Version()
        if err != nil {
                panic(err)
        }
        fmt.Printf("Connected to zabbix api v%s\n", res)
}
```

## Tests

### Considerations

You should run tests before using this package.
The Zabbix API doesn't match the documentation in a few details, which are changing in patch releases.

Tests are not expected to be destructive, but you are advised to run them against not-production instance or at least make a backup.
For a safer and more accurate testing we advice to run tests with following minimum versions which implements strict validation of valuemap for `get` method:

For more information, please see issues [ZBX-3783](https://support.zabbix.com/browse/ZBX-3783) and [ZBX-3685](https://support.zabbix.com/browse/ZBX-3685)

### Run tests

```bash
export TEST_ZABBIX_URL=http://localhost:8080/zabbix/api_jsonrpc.php
export TEST_ZABBIX_USER=Admin
export TEST_ZABBIX_PASSWORD=zabbix
export TEST_ZABBIX_VERBOSE=1
go test -v
```

`TEST_ZABBIX_URL` may contain HTTP basic auth username and password: `http://username:password@host/api_jsonrpc.php`. Also, in some setups URL should be like `http://host/zabbix/api_jsonrpc.php`.

## References

Documentation is available on [godoc.org](https://godoc.org/github.com/tpretz/go-zabbix-api).
Also, Rafael Fernandes dos Santos wrote a [great article](http://www.sourcecode.net.br/2014/02/zabbix-api-with-golang.html) about using and extending this package.

License: Simplified BSD License (see [LICENSE](LICENSE)).
