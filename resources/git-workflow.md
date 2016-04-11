# Working with Git

One thing we love about DuckDuckHack is that it's frequently people's first open-source contribution. If that's the case for you, you might be encountering *Git* for the first time. **Git is a tool that allows many people to collaborate on one codebase.**

At DuckDuckHack, we have several Git repositories (hosted on GitHub.com), which reflect the current state of Instant Answer code. The Instant Answers that run on DuckDuckGo.com come directly from these repositories.

The two main repositories are Goodies and Spice. There's no particular reason to divide it this way, except that Goodies don't make external requests, and Spice Instant Answers do.

- [The Goodie Repository](https://github.com/duckduckgo/zeroclickinfo-goodies)
- [The Spice Repository](https://github.com/duckduckgo/zeroclickinfo-spice)

**The following is an overview of how you'll use Git to contribute to DuckDuckHack.** This is the workflow used by all of our contributors worldwide to collaborate on Instant Answers. If you prefer, you can also watch a [video screencast of this process](https://vimeo.com/148366187).

<iframe src="https://player.vimeo.com/video/148366187?byline=0" width="757" height="425" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

----

## Step 1: Fork the Repository

Your ultimate goal is to add code to the Spice repository, in this case. To do that, you'll first make a copy that you can freely modify. That's called ["forking a repository"](https://help.github.com/articles/fork-a-repo/).

(Find out how to do this under [setting up your development environment](http://docs.duckduckhack.com/welcome/setup-dev-environment.html).)

## Step 2: Clone Your Fork of the Repository

Forking on GitHub means you've made a copy up on your GitHub account. However, to edit files, you'll need to [*clone*](https://help.github.com/articles/cloning-a-repository/) that fork to a machine you can access. In our case, that will be your [Codio environment](http://docs.duckduckhack.com/welcome/setup-dev-environment.html).

(Find out how to do this under [setting up your development environment](http://docs.duckduckhack.com/welcome/setup-dev-environment.html).)

## Step 3: Create a Working Branch for Coding

Inside your repository, Git allows you to work on parallel versions of your code. These are called ["branches"](https://www.atlassian.com/git/tutorials/using-branches/). You can think of a  branch is an "independent line of development."

Every repository starts with one, default branch called `master`. It's best to keep `master` clean of changes, and instead work off of *new, separate branches*. This allows you to keep `master` constantly updated with the original repo (covered in Step #5, below). 

Creating new branches also allows you to work on multiple submissions at the same time while keeping them separate from one another.

Make a new branch by typing:

```
git checkout -b my-new-branch
```

This will create a new branch and also switch into it.

You can switch back to `master` by typing:

```
git checkout master
```

and back to your new branch the same way.

**Keep a separate working branch for each Instant Answer you're working on.** This allows you to keep the changes separate. That way any hold-ups on one Instant Answer won't delay acceptance of another.


## Step 4: Make Your Changes

Add your new Instant Answer to the repository, test it, and play around. Or, make changes to an existing Instant Answer. This is the fun part!

Make sure to [commit](https://www.atlassian.com/git/tutorials/saving-changes/git-commit) your changes along the way. **"Committing" is the most important action in Git.** It's like saving a snapshot of your project at various milestones. You should commit often, to mark units of achievement - however small!

Committing involves first staging all your changes with `git add .`, then committing them with `git commit`. We recommend [this great tutorial](https://www.atlassian.com/git/tutorials/saving-changes) on how to use both. In short, type:

```
git add .
git commit -m '<brief commit description>'
```

## Step 5: Update your local repository with any changes made by other contributors

While you're working, many other developers around the world have been busy merging changes to the original repository. Most likely there won't be overlap, but there may be some *[merge conflicts](https://help.github.com/articles/resolving-a-merge-conflict-from-the-command-line/)* if two people have made changes to the same Instant Answer.

**It's best practice to start each work session by updating *your* fork with the latest changes.** This is one major reason we kept `master` free of changes. We can use it as an ongoing reflection of the original repository's master branch.

First, you'll need to add a 'remote' that points to the original, main repository. We'll call it upstream. (Github's equivalent [instructions](https://help.github.com/articles/configuring-a-remote-for-a-fork/)).

```
git remote add upstream https://github.com/duckduckgo/zeroclickinfo-xxxxx.git
```

Next, to update your `master` branch, `git checkout` the branch, and type:

```
git pull upstream master
```

This will pull the changes from the latest `master` branch into yours, so you’re up-to-date. (GitHub's equivalent [instructions](https://help.github.com/articles/syncing-a-fork/).)

Next, to update your *working branches* off of `master`, [merge or rebase](https://www.atlassian.com/git/tutorials/merging-vs-rebasing/) with the `master` branch.

If you encounter any merge conflicts, don't sweat: [GitHub has a great guide](https://help.github.com/articles/resolving-a-merge-conflict-from-the-command-line/) for how to resolve them.

## Step 6: Make a Pull Request

Ready to submit your work? It's time to make a *[pull request](http://oss-watch.ac.uk/resources/pullrequest)* on the original repository.

A [pull request](http://oss-watch.ac.uk/resources/pullrequest) is the process of submitting changes to a collaborative project. It's your way of asking that the changes made on **your fork** be incorporated into the **original repository**.

*Because we're focusing on Git, we'll gloss over the [guidelines](http://docs.duckduckhack.com/submitting/checklist.html) for making a pull request. If you're working on a real Instant Answer, you'll want to learn more [about the process for going live](http://docs.duckduckhack.com/submitting/submitting-overview.html).*

The first step to making a pull request is updating the clone of your repository that lives up on GitHub.com. Go to the branch you're working on, and type:

```
git push origin my-branch-name
```

This updates the equivalent branch on GitHub.com. Next, visit your repository on GitHub.com. Find the branch you just pushed. Finally, click the **Pull Request** button. GitHub has [excellent instructions](https://help.github.com/articles/using-pull-requests/) on how to do this on their site.

## Step 7: Update Your Pull Request

Once created, your pull request page will be the center of feedback and discussion of your changes. **You can continue to make ongoing changes to your pull request.** Simply keep making commits - and push them your fork on Github - and the pull request will update automatically. (This is another reason it's critical to keep contributions separate on different branches: it keeps pull requests clean of unrelated changes.)

[![slack](http://docs.duckduckhack.com/assets/slack.png) Have questions about git? Talk to us on Slack]({{ book.slackURL }}) or [email us](mailto:open@duckduckgo.com).
