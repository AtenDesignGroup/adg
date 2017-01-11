ADG
====
The standard Aten Design Group CLI

`adg` is the (attempted) universal command line utility for common actions.

**NOTE**: This is a just design document at the moment.

## Idea
Dropped into any project, a custom implementation or a generalized version of `adg` using a configuration file should exist. The same common commands, regardless of project details should perform similar commands.

It is permissible for a command to be unimplemented, but it is _not_ permissible to have a _different_ command or README for doing things which `adg` could accomplish.

## Subcommands
```
deploy 
test
requirements
```

### Usage
- `deploy`
  - `deploy [environment] [<subproject>]
