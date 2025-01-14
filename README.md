# tpl

tpl is build for generating config files from templates using simple or complex (lists, maps, objects) shell environment 
variables. Since the binary has zero dependencies it is build for docker but you can use it across all platform and 
operating systems.

tpl uses [sprig](https://github.com/Masterminds/sprig) to extend golang's template capabilities.

See test section and have a look at `test.tpl` (template) and `text.txt` (result) in test folder for examples.

## setup

Just download the binary for your OS and arch from the [releases](https://github.com/schneidexe/tpl/releases) page. 

If you want to use it inside your docker image you can add this to your `Dockerfile`:

```
RUN curl -sL https://github.com/schneidexe/tpl/releases/download/v0.4.6/tpl-linux-amd64 -o tpl && \
    chmod a+x tpl
```

## build 
```
go get github.com/mitchellh/gox
gox -arch="386 amd64" -os="darwin linux windows"
```

## test
```
export foo="bar"
export bar="[foo,bar]"
export foobar="{foo:bar,bar:foo,url:\"http://foo.bar\"}"
export foobaz="{foo:[bar,baz]}" 
export baz="1.0-123"
export number="59614658972"
export null="null"
export empty=
export money="500€"
export special="?&>=:/"
export woot="[]"
export whoa="{}"

go get -v
go run tpl.go -t test/test.tpl | diff - test/test.txt && echo Tests succeeded! || echo Tests failed!
```
