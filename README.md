ADG
====
The standard Aten Design Group CLI

`adg` is the (attempted) universal command line utility for common actions.

**NOTE**: This is a just design document at the moment.

## Idea
Dropped into any project, a custom implementation or a generalized version of `adg` using a configuration file should exist. The same common commands, regardless of project details should perform similar commands.

It is permissible for a command to be unimplemented, but it is _not_ permissible to have a _different_ command or README for doing things which `adg` could accomplish.

```
adg [command] [--help] [...<args>]
```

## Commands
```
deploy 
test
requirements
```

### Usage
- `deploy`
  - `deploy [environment] [...<application>]`
  - `environment`: `dev`, `test`, or `prod`. Others may exist but may not use a synonym. For example, you cannot use `stage` instead of `test` but you may have `dev0` and `dev1`
  - `application` _optional._ In some cases, there may be more than one application that needs to be deployed within a project. In this case, you may require an application name to be specified. In this case, an implementation should provide an `all` shorthand to deploy all applications within a project with one command.
- `test`
  - `test [...<args>]`
  - `args` _optional._ The basic implementation of the test command should run all tests. However, an implementation may require a additional commands to be specified. These commands must be documented by: `adg test --help`
- `requirements`
  - `requirements`
  - Requirements should take no arguments, it should return a message outlining requirements to run the application locally. An implementation may attempt to verify that requirements are met by the local system. For example, it may do `which docker` to see if docker is installed.
