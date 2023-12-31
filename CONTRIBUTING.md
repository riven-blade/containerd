# Contributors' Guide

This guide will help familiarize contributors to the `containerd/containerd` repository.

## Prerequisite

First read the containerd project's [general guidelines around contribution](https://github.com/containerd/project/blob/main/CONTRIBUTING.md)
which apply to all containerd projects.

## Getting started

See [`BUILDING.md`](https://github.com/containerd/containerd/blob/main/BUILDING.md) for instructions for setting up a development environment.

If you are also a new user to containerd, you can first check out the [_Getting started with containerd_](https://github.com/containerd/containerd/blob/main/docs/getting-started.md) guide.

## Setting up your local environment

At a minimum, the dev tools from `script/setup/install-dev-tools` should be installed.
Run `make install-deps` to install dependencies used for running and developing the CRI plugin.
Other install scripts under `script/setup` may need to be run depending on your environment and your preference for installing libraries and dependencies.
The versions used by `containerd/containerd` CI can be found in `script/setup` and referred to if installing manually.

```
$ script/setup/install-dev-tools
$ make install-deps
```

## Code style

- Go files adhere to standard Go formatting and styling
- Protobuf files use tabs for indentation
- Other files must not contain trailing whitespace and should end with a single new line character

Use the `check` command in the makefile to verify your code matches the expected style.

```
make check
```

## Updating protobuf files

Ensure protoc and dev tools have been installed, then run `make protos`

> **Note**
> When running `make protos`, the current working directory should be found under the `GOPATH` environment
> variable to ensure protoc can properly resolve the paths of protofiles in the project.

## Naming packages

Package names should be short and simple. Avoid using `_` and repeating words from parent directories.

### Where to put packages

Try to put a new package under the appropriate root directories. The root directory is reserved for
configuration and build files, no source files will be accepted in root since containerd v2.0.

- `api` - All protobuf service definitions and types used by services
- `bin` - Autogenerated during build, do not check in file here
- `client` - All Go files for the containerd client (formerly in `containerd/containerd` root in 1.x)
- `cmd` - All Go main packages and the packages used only for that main package
- `contrib` - Files, configurations, and packages related to external tools or libraries
- `docs` - All containerd technical documentation using markdown
- `man`- All containerd reference manuals used for the `man` command
- `pkg` - All Go packages shared and used by other containerd packages.
- `plugins` - All included containerd plugins which are registered via init
- `releases` - All release note files
- `script` - All scripts used for testing, development, and CI
- `test` - Test scripts used for external end to end testing of containerd, do not add new files here
- `vendor` - Autogenerated vendor files from `make vendor` command, do not manually edit files here
- `version` - Version package with the current containerd version
