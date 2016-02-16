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

This will lead you through a dialogue and generate the minimum necessary files with proper naming conventions. This command will only work inside a Goodie or Spice repository, and generate the corresponding Instant Answer.

The `duckpan new` command has several preset file templates you can choose from. To choose a particular preset template: 

```shell
duckpan new --template TEMPLATE_NAME
```

> The word 'template' in this context refers to file configurations, not frontend HTML templates or template groups. The terminology is admittedly confusing.

In the Goodie repository, your options for `TEMPLATE_NAME` are:

- **`default`** - creates the basic file types you might need in your Goodie: a Perl file and a test file, both in their correct directories.	
- **`cheatsheet`** - creates the single necessary JSON file for a cheatsheet in the correct directory. For more information see the [cheat sheets reference](http://docs.duckduckhack.com/frontend-reference/cheat-sheet-reference.html).
- **`javascript`** - creates a JavaScript-heavy Goodie (i.e. where most of the functionality is on the frontend), including a minimal Perl file, a frontend JavaScript file, and a test file.
- **`all`** - creates all possible file types you might need in your Goodie: Perl, test file, Javascript file, CSS file, and a Handlebars file, all in their correct directories. *It's useful to start with this option, then delete files you don't use.*

In the Spice repository, your options for `TEMPLATE_NAME` are:

- **`default`** - creates the basic file types you might need in your Spice: Perl, test file, and Javascript file, all in their correct directories.	
- **`all`** - creates all possible file types you might need in your Spice: Perl, test file, Javascript file, CSS file, and a Handlebars file, all in their correct directories. *It's useful to start with this option, then delete files you don't use.*

You'll also be prompted to add additional template files if you so please. This allows you to selectively add particular boilerplate file types:

```
Would you like to configure optional templates? [y/N]: y                                                                              
                                                                                                                                      
  1> Javascript                                                                                                                       
  2> CSS                                                                                                                              
  3> Handlebars                                                                                                                       
  4> Javascript, CSS                                                                                                                  
  5> Javascript, Handlebars                                                                                                           
  6> CSS, Handlebars                                                                                                                  
  7> Javascript, CSS, Handlebars                                                                                                      
                                                                                                                                      
Choose configuration [1]:
```

DuckPAN's configurability is rather new, and we look forward to add more templates and configurations in the future. We'd love to [hear your thoughts](http://docs.duckduckhack.com/resources/get-in-touch.html) and ideas for how to make this feature more useful to you!

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


