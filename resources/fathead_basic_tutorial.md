# Basic Fathead Tutorial

In this tutorial, we'll be making a Fathead Instant Answer that shows example source code for a "Hello World" program in whatever language is specified by the user's query. The live Instant Answer looks like this: https://duckduckgo.com/?q=hello+world+scala. As discussed in [the Fathead overview](/duckduckhack/fathead_overview), our goal is to generate an output.txt, which will look something like this:

###### output.txt (snippet)

```
hello world (python)	A										Hello World in python (python.py)<br>#!/usr/bin/env python\nprint "Hello World"\n	https://github.com/leachim6/hello-world
hello world (postscript page)	A										Hello World in postscript_page (postscript_page.ps)<br>% run> gs -q postscript_page.ps\n/pt {72 div} def\n/y 9 def\n/textdraw {/Courier findfont 12 pt scalefont setfont 8 pt y moveto show} def\n\n72 72 scale\n0 0 0 setrgbcolor\n\n(Hello world!) textdraw\nshowpage\nquit	https://github.com/leachim6/hello-world
hello world (perl)	A										Hello World in perl (perl.pl)<br>#!/usr/bin/perl\nprint "Hello World\\n";\n	https://github.com/leachim6/hello-world
```

## Step 1: Write Perl module

To begin, use your favourite text editor like [gedit](http://projects.gnome.org/gedit/), notepad, or [emacs](http://www.gnu.org/software/emacs/) to open `lib/DDG/Fathead/HelloWorld.pm` and type the following:

```perl
package DDG::Fathead::HelloWorld;
# ABSTRACT: Provides an example "Hello World" program for a given programming language
```

Next, type the following [use statement](https://duckduckgo.com/?q=perl+use) to import [the magic](https://github.com/duckduckgo/duckduckgo/tree/master/lib/DDG) behind our Instant Answer system.

```perl
use DDG::Fathead;
```

Next, we'll add some metadata fields. These should be self-explanatory, but for more information, please refer to [Metadata](/duckduckhack/metadata).

```perl
primary_example_queries "hello world perl";

secondary_example_queries
    "javascript hello world",
    "hello world in c";

description "Hello World programs in many program languages";

name "HelloWorld";

icon_url "/i/www.github.com.ico";

source "GitHub";

code_url "https://github.com/duckduckgo/zeroclickinfo-fathead/tree/master/share/fathead/hello_world";

topics "geek", "programming";

category "programming";

attribution
    twitter => ['https://twitter.com/jperla', 'jperla'],
    web => ['http://www.jperla.com/blog', 'Joseph Perla'];
```

Finally, all Perl packages that load correctly should [return a true value](http://stackoverflow.com/questions/5293246/why-the-1-at-the-end-of-each-perl-package) so add a 1 on the very last line, and make sure to also add a newline at the end of the file.

```perl
1;

```

Our Perl package is now complete. The entire file should look like this:

```perl
package DDG::Fathead::HelloWorld;
# ABSTRACT: Provides an example "Hello World" program for a given programming language

use DDG::Fathead;

primary_example_queries "hello world perl";

secondary_example_queries
    "javascript hello world",
    "hello world in c";

description "Hello World programs in many program languages";

name "HelloWorld";

icon_url "/i/www.github.com.ico";

source "GitHub";

code_url "https://github.com/duckduckgo/zeroclickinfo-fathead/tree/master/share/fathead/hello_world";

topics "geek", "programming";

category "programming";

attribution
    twitter => ['https://twitter.com/jperla', 'jperla'],
    web => ['http://www.jperla.com/blog', 'Joseph Perla'];

1;

```

## Step 2: Create a directory

Every Fathead has a directory under share/fathead/ that contains all files except the one we just created. The name of the directory must be the name of the Perl module converted to [snake case](https://en.wikipedia.org/wiki/Snake_case). For this tutorial, we'll use `share/fathead/hello_world/`.

## Step 3: Write the fetch.sh script

Every Fathead Instant Answer requires a `fetch.sh` file. This shell script is invoked to fetch the remote data that we need in order to generate our output. For example, following script will clone a git repository that contains a collection of hello world source files:

###### share/fathead/hello_world/fetch.sh

```shell
#!/bin/sh

git clone git://github.com/leachim6/hello-world.git download
```

In this case, the git repository is just a collection of source files; we'll need to do some parsing in order to get it into the format we need. Note that *git clone* is not the only way to fetch data. Most Fatheads use *curl* or *wget*.

**Also Note:** All temporary files should be placed in the `download/` subdirectory within your Fathead's directory. For this example, that means `share/fathead/hello_world/download/`. *git* creates this subdirectory for us, but if your plugin uses a different tool, you make have to include `mkdir download` in your fetch script.

## Step 4: Write the parsing script

The data we just fetched needs to be parsed before we can use it, so we'll write a script to do that. Parse scripts can be written in any language, but please use a common language like Perl, Python, JavaScript, Go, or similar. The harder your script is to run, the harder it will be for us to integrate your Instant Answer into our environment, and the harder future maintenance will be. **Please keep things as simple and straightforward as possible.**

**Note:** Our machines are running **Ubuntu 12.04**. These are the machines that will be used to test and run your parser, so **please make sure your language and dependencies are compatible with our environment**.

Since Fatheads can have vastly different data sources, we can't tell you what is the best approach to parsing. We suggest you look through the [Fathead repository](https://github.com/duckduckgo/zeroclickinfo-fathead/tree/master/share/fathead) to get ideas from other developers.

For the purposes of this tutorial, we're going to use Python to parse the git repository we just cloned.

###### share/fathead/hello_world/parse.py

```python
if __name__ == "__main__":
    # setup logger
    logging.basicConfig(level=logging.INFO,format="%(message)s")
    logger = logging.getLogger()

    # dump config items
    count = 0
    with open("output.txt", "wt") as output_file:
        for filepath in glob.glob('download/*/*'):
            _,filename = os.path.split(filepath)
            # ignore some "languages"
            if filename not in ['ls.ls', 'readlink.readlink', 'piet.png']:

                language,_ = os.path.splitext(filename)
                with open(filepath, 'r') as f:
                    source = f.read()
                source = source.replace('\\n', '~~~n')
                source = source.replace('\n', '\\n')
                source = source.replace('~~~n', '\\\\n')
                source = source.replace('\t', '\\t')

                item = HelloWorldItem(language, filename, source)
                if count % 10 == 0:
                    logger.info("%d languages processed" % count )

                count += 1
                output_file.write(str(item))
    logger.info("Parsed %d domain rankings successfully" % count)
```

This uses a relatively simple loop, `for filepath in glob.glob('download/*/*'):` which iterates over each of the files in the repository our fetch script cloned into the `download/` directory. After doing some checks to make sure the files is a "Hello World" program, it opens the file, reads the file, escapes newline (`\n`) and tab (`\t`) characters and then then "parses" the file to create an `item` using the `HelloWorldItem` class:

###### parse.py (continued)

```python
class HelloWorldItem:
  def __init__(self, language, filename, source):
    self.language = language
    self.filename = filename
    self.source = source

  def __str__(self):

    fields = [ "hello world (%s)" % self.language,  #title
               "A", #type
               "",
               "",
               "",  #categories
               "",
               "",  #see_also
               "",
               "",  #external_links
               "",
               "",  #images
               "Hello World in %s (%s)<br>%s" % (self.language, self.filename, self.source),
               "https://github.com/leachim6/hello-world"
             ]

    output = "%s\n" % ("\t".join(fields))

    return output
```

The `HelloWorldItem` class works by defining the string representation of itself, which we later use to print our object into `output.txt`: `output_file.write(str(item))`.

The most important thing to note about the string representation function, `def __str__(self):`, is that it creates an array containing the relevant information we need to pass along to `output.txt`, which **includes a few blank lines to represent the optional output fields we have not used** and then joins them with tab characters (`\t`). It also appends a newline (`\n`) at the end of our built string. This string now represent a single line in our `output.txt` file and denotes the **title**, **abstract**, **synopsis** and the **source_url**.

## Step 5: Write a wrapper for the parse script

Since the parse script can be written in any language, we use a thin wrapper called `parse.sh` so we have a consistent name to execute. This is easy:

###### parse.sh

```shell
#!/bin/sh

python parse.py
```

## Step 6

The last thing we need to write is a README.txt. This file is used to inform other developers and DuckDuckGo staff of any special considerations. At the very least, it should list dependencies required by your parse script. You may also want to mention known shortcomings, opportunities for future improvement, or anything else you think might be important.

###### README.txt

```
Dependencies:

Python 3

To install in Ubuntu 10.04 (Lucid):

sudo apt-get install python3-minimal
```

## Step 7

You're done! The only thing left is to submit your Instant Answer for review. Please see [Preparing for a Pull Request](/duckduckhack/preparing_for_a_pull_request).

**Note:** The duckpan server cannot (currently) run Fatheads. That means you can't run or test your plugin before submission.

