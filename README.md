# go-workspace

This a repo following the guide on go workspaces here:

https://go.dev/doc/tutorial/workspaces

More info about workspaces can also be found here:

https://go.dev/ref/mod#workspaces

# Main concepts

- `go.work` can be used to tell the Go command that you’re writing code in 
multiple modules at the same time and easily build and run code in those modules. This way, you can `build` and `run`
code from the different submodules (hello, example) without having to go into each folder/module separately. The 
workspace acts a single module, composed by one or more submodules.
- `go.work` can be used instead of adding replace directives to work across multiple modules. In the `example` folder
we customized the code of https://go.googlesource.com/example and told the Go command to use the local copy instead
of fetching and using the remote repository.
- When no `go.work` file exists, the workspace consists of the single module containing the current directory.
- `go.work` files also allow to specify replaces to other upstream modules via the replace directive.

# Demo

1. Run the hello module from the workspace, making use of the `go.work` file and the modifications in the `example` folder
over the https://go.googlesource.com/example module.

```shell
go run github.com/lopezator/go-workspace/hello
```

Returns: `HELLO`.

2. Remove the `./example` line from the `go.work` file and run again the hello module.

```shell
go run github.com/lopezator/go-workspace/hello
```

This fails, because the `ToUpper` function is not present in the upstream module https://go.googlesource.com/example

```
go run github.com/lopezator/go-workspace/hello
# github.com/lopezator/go-workspace/hello
hello/hello.go:10:25: undefined: stringutil.ToUpper
```