# Building and Testing

### Building and Testing <a href="#building-and-testing" id="building-and-testing"></a>

Developers should use a recent version of Go for building and testing. We use the go toolchain for development, which you can get from the [Go downloads page](https://golang.org/doc/install). Geth is a Go module, and uses the [Go modules system](https://github.com/golang/go/wiki/Modules) to manage dependencies. Using GOPATH is not required to build go-ethereum.

#### Building Executables <a href="#building-executables" id="building-executables"></a>

Switch to the go-ethereum repository root directory. All code can be built using the go tool, placing the resulting binary in $GOPATH/bin.

```sh
go install -v ./...
```

go-ethereum executables can be built individually. To build just geth, use:

```sh
go install -v ./cmd/geth
```

Cross compilation is not recommended, please build Geth for the host architecture.

#### Testing <a href="#testing" id="testing"></a>

Testing a package:

```sh
go test -v ./eth
```

Running an individual test:

```sh
go test -v ./eth -run TestMethod
```

**Note**: here all tests with prefix _TestMethod_ will be run, so if TestMethod and TestMethod1 both exist then both tests will run.

Running benchmarks, eg.:

```sh
go test -v -bench . -run BenchmarkJoin
```

For more information, see the [go test flags](https://golang.org/cmd/go/#hdr-Testing\_flags) documentation.



