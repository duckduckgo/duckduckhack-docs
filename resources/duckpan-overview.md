# The DuckPAN Tool

DuckPAN is a command line interface to help developers build, test, and configure their Instant Answers. It is available by default in the [Codio terminal](http://docs.duckduckhack.com/welcome/setup-dev-environment.html).

## Using DuckPAN

### Help Commands

```shell
duckpan
```

or

```shell
duckpan help
```

or

```shell
man duckpan
```

Prints out the DuckPAN man page

### Instant Answer Boilerplate

```shell
duckpan new
```

This will lead you through a dialogue and generate boilerplate files with proper naming conventions. This command will only work inside a Goodie or Spice repository. To see this in action, visit any of the Instant Answer walkthroughs.

### Instant Answer Testing

```shell
duckpan query
```

Test Goodie and Spice triggers interactively on the command line. Typing a query here is just like using DuckDuckGo.com, except you're only viewing the server response, and in its raw form. Learn more about [interactive testing](http://docs.duckduckhack.com/testing-reference/testing-triggers.html).


```shell
duckpan server [--verbose] [--no-cache] [--port <number>]
```

Test Goodie and Spice Instant Answers on a local web server (for design/layout purposes)

Options:

- `--verbose` to provide more details
- `--no-cache` to prevent DuckPAN's cache from being used (this forces the requested files to be pushed into the cache)
- `--port` to specify which port DuckPAN's server should run on (defaults to 5000)


### Configuration Commands

```shell
duckpan env
```

View env commands and also shows the env variables currently stored in ~/.duckpan/env.ini

```shell
duckpan env <name> <value>
```

Add an environment variable that duckpan will remember. Useful for
spice API keys. Variables are stored in ~/.duckpan/env.ini

```shell
duckpan env <name>
```

Retrieve the matching key for a given env variable.

```shell
duckpan env rm <name>
```

Remove an environment variable from duckpan

```shell
duckpan release
```

Release the project of the current directory to DuckPAN

### Advanced Install Commands

```shell
duckpan installdeps
```

Install all requirements of the specific DuckDuckHack project (if
possible), like zeroclickinfo-spice, zeroclickinfo-goodie, duckduckgo
or community-platform

```shell
duckpan roadrunner
```

Same as `installdeps`, but avoids testing anything. Useful for speed, but
not recommended unless you know what you are doing.

```shell
duckpan check
```

Check if you fulfill all requirements for the development
environment (this is run automatically during setup)

```shell
duckpan reinstall
```

Force installation of the latest released versions of DuckPAN and DDG


