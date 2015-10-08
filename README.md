sample-golang-packaging
=======================

## Description

Trying out `gb` build/package management tools.

- http://getgb.io/
- https://github.com/constabulary/gb
- https://godoc.org/github.com/constabulary/gb/cmd/gb-vendor
- http://go-talks.appspot.com/github.com/davecheney/presentations/reproducible-builds.slide


## Installation

```
$ brew update
$ brew upgrade go
$ go version
go version go1.5.1 darwin/amd64
```

Put these lines in `.zshrc` and `source`.

```
# for golang
export GOVERSION=1.5.1
export GO15VENDOREXPERIMENT=1
export GOPATH=$HOME/.go/$GOVERSION
export GOROOT=/usr/local/Cellar/go/$GOVERSION/libexec
export PATH=$GOPATH/bin:$PATH
```


```
go get github.com/constabulary/gb/...
```


## Install dependencies

```
$ gb vendor fetch github.com/fatih/color
```

`color` will be installed in `vendor` package


## Build

```
$ gb build all
```


## Execute

```
$ ./bin/helloworld
Hello, world!
```


## Manifest

```
$ cat vendor/manifest
{
        "version": 0,
        "dependencies": [
                {
                        "importpath": "github.com/fatih/color",
                        "repository": "https://github.com/fatih/color",
                        "revision": "76d423163af754ff6423d2d9be0057fbf03c57c2",
                        "branch": "master"
                },
                {
                        "importpath": "github.com/mattn/go-isatty",
                        "repository": "https://github.com/mattn/go-isatty",
                        "revision": "7fcbc72f853b92b5720db4a6b8482be612daef24",
                        "branch": "master"
                },
                {
                        "importpath": "github.com/shiena/ansicolor",
                        "repository": "https://github.com/shiena/ansicolor",
                        "revision": "d445752f6f66f9cd987722f109149f6799cdf1de",
                        "branch": "master"
                }
        ]
}%
```

## Install dependencies using manifest file

Cleaning up project

```
$ rm -rf bin pkg
$ rm -rf vendor/src
```

```
$ gb vendor restore
Getting github.com/fatih/color
Getting github.com/mattn/go-isatty
Getting github.com/shiena/ansicolor
```

```
$ gb build all
$ ./bin/helloworld
Hello, world!
```
