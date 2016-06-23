# gluaenv

Utility package for manipulating environment variables for [gopher-lua](https://github.com/yuin/gopher-lua)

## Installation

```
go get github.com/kohkimakimoto/gluaenv
```

## API

* `env.set(key, value)`
* `env.get(key)`
* `env.loadfile(file)`

## Usage

```go
package main

import (
    "github.com/yuin/gopher-lua"
    "github.com/kohkimakimoto/gluaenv"
)

func main() {
    L := lua.NewState()
    defer L.Close()

    L.PreloadModule("env", gluaenv.Loader)
    if err := L.DoString(`
local env = require("env")

-- set a environment variable
env.set("HOGE_KEY", "HOGE_VALUE")

-- get a environment variable
local v = env.get("HOGE_KEY")

-- load envrironment variables from a file.
env.loadfile("path/to/.env")

-- file example
-- AAA=BBB
-- CCC=DDD

`); err != nil {
        panic(err)
    }
}
```
