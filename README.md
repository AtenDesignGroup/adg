ADG
====
The standard Aten Design Group CLI

`adg` is the (attempted) universal command line utility for common actions.

**NOTE**: This is a just design document at the moment.

## Idea
Dropped into any project, a custom implementation or a generalized version of `adg` using a configuration file should exist. The same set of common commands, regardless of project details, should perform similar actions. By specifyin a protocol for such a command, rather than a concrete implementation we can retroactively provide implementations to old projects and/or move to new or differing technologies over time.

## Specification

It is permissible for a command to be unimplemented, but it is _not_ permissible to have a _different_ command or README for doing things which `adg` could accomplish.

Messages and logs **MUST** be written to `stderr`. Failed operations **MUST** exit with a non-zero exit code. Succesful operations **MUST** exit with the exit code `0`.

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
  - `deploy [--list-environments] [environment] [--list-applications] [...<application>]`
  - `--list-environments` **MUST** return a list of the available environments. If any are _not implemented_ an implementation **MUST NOT** return those environment names.
  - `environment`: `dev`, `test`, or `prod`. Implementations **MUST** use these names. If more names are needed an implementation **MAY** provide additional names. However, an implementation **MUST NOT** provide use names which are synonyms of the aforementioned names. I.E. A server cannot have the name `stage` instead of `test`.
  - `--list-applications` **MUST** return a list of the available applications to deploy _for the given environment_. If any are _not implemented_ an implementation **MUST NOT** return those application names.
  - `application` _optional._ In some cases, there may be more than one application that needs to be deployed within a project. In this case, an implementation **MAY** require an application name to be specified. In that case, an implementation **SHOULD** provide an `all` shorthand to deploy all applications within a project with a single command.
- `test`
  - `test [type] [...<args>]`
  - `type` An implementation **MUST** implement `js` and/or `php` if tests for those languages exist. Additional test types are permitted. An implementation **MUST NOT** use synonyms for these types. I.E. an implementation cannot define `frontend` as a test type.
  - `args` _optional._ This allows custom arguments to be passed through to the underlying test runners like `ava` or `phpunit`. An implementation **MAY** provide default args.
- `requirements`
  - `requirements`
  - Requirements **MUST** take no arguments, it **MUST** return a message outlining requirements to run the application locally. An implementation **MAY** attempt to verify that requirements are met by the local system. For example, it **MAY** do `which docker` to see if docker is installed.
