# Setting Up Your Development Environment

In order to get moving with Instant Answer development, you'll need to setup your environment. There are three main steps: 

1. Fork the Spice Repository on Github.com
2. Fork the DuckDuckGo environment on Codio.com
3. Clone your Github fork onto the Codio environment

You can also watch a [video screencast of this tutorial](https://vimeo.com/132712266).

![https://vimeo.com/132712266](https://talsraviv.gitbooks.io/duckduckhackdocs/content/duckduckhack/assets/screencast_environment-setup.jpg)

## 1. Sign Up for Github.com

*Already have a GitHub Account? Perfect, move to the next step.*

Git is a tool that allows many people to collaborate on one codebase. GitHub is a popular site for groups to host Git repositories. If this is your first time using Git and GitHub, we've created an [overview of how you'll use Git](https://talsraviv.gitbooks.io/duckduckhackdocs/content/duckduckhack/resources/git-workflow.html) to contribute to DuckDuckHack.

To get started, let's sign up for GitHub:

1. Go to https://github.com/join and enter the required information, then click "**Create an Account**"
2. Click "**Finish Signup**" to continue with a **Free** GitHub account.

## 2. Set Up Your DuckDuckGo Environment on Codio.com

Aside from the Instant Answer code files, we need a machine that can *run and test* these files. We use Codio.com as a very convenient way to help contributors set up a fresh, ready-to-run environment in a matter of clicks.

### Sign up for a Codio Account

*Already have a Codio Account? Perfect, move on to [the next step](#fork-the-duckduckhack-project-on-codio)!*

1. Go to https://codio.com and click "**Get Started**", at the top right corner.
2. Click "**Sign Up via GitHub**".
3. If you aren't already signed into GitHub, enter your GitHub login details and then click "**Sign In**".
4. Click "**Authorize application**" to continue.
5. In the new screen, enter the required details and click "**Create Account**".

### Create Your Own DuckDuckHack Machine

In this step we'll setup our virtual development computer with all the convenient development tools pre-installed. We've already created this for you on Codio, and all you need to do is make a copy for yourself.

1. **After logging into Codio,** [click this link](https://codio.com/p/signup?orgToken=Ax-OB3tU4sdNAG8axJBYcjNqR04) and you'll be added to our organization, which gives you a professional Codio setup free of charge. 

	You should see a confirmation message at the bottom of your Codio screen after clicking.

2. Go to https://codio.com/duckduckgo/duckduckhack and click "**Project**" at the top left corner.

3. In the drop-down, select the "**Fork**" option.

    ![Codio Fork](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckpan%2Fassets%2Fcodio_fork.png)

4. In the pop-up window, select the "**Box & Project**" option and click "**Continue**".

    ![Codio Fork Both](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckpan%2Fassets%2Fcodio_fork_both.png)

5. Wait a minute while the project forks...

6. You should now see a new window with three panes. It should say "**DuckDuckHack**" at the top of the left pane.

Good work! You now have your own machine on Codio with all the DuckDuckHack development tools installed. You'll learn more about these tools in the tutorials.

## 3. Clone your Github fork onto your Codio Machine

The final step is to obtain the latest copy of the open-source code powering all Instant Answers. We're going to "fork" that code, so you'll have your own personal copy which you can modify and test.

The two main repositories are Goodies and Spice. There's no particular reason to divide it this way, except that Goodies don't make external requests, and Spice Instant Answers do.

- [The Goodie Repository](https://github.com/duckduckgo/zeroclickinfo-goodies)
- [The Spice Repository](https://github.com/duckduckgo/zeroclickinfo-spice)

1. Make sure you are logged in to Github.com as yourself

2. Go to the corresponding Instant Answer repository homepage:

    - [Goodies](https://github.com/duckduckgo/zeroclickinfo-goodies) (for Cheat Sheets, and Instant Answers that are pure code functions)
    - [Spice](https://github.com/duckduckgo/zeroclickinfo-spice) (for Instant Answers that will make API calls) 

	Don't worry about picking the right one: you can fork either or both of these repositories - just repeat these steps.
	
3. Click "**Fork**", near the top-right corner.
	
	Wait while the repo forks...

4. You should see a page that looks nearly identical to the repo home page you were just on. The URL should be different though, it should look like **`https://github.com/yourGitHubUsername/zeroclickinfo-xxxxx`**. 

	**This is the URL for your personal copy of the DuckDuckHack code. Keep it handy, we'll be using it in a minute!**

## Clone your Github Repository onto your Codio Machine

Forking on Github means you've made a copy up on your Github account. However, to edit files, you'll need to [*clone*](https://help.github.com/articles/cloning-a-repository/) that fork to a machine you can access. In our case, we'll clone it to our Codio environment:

1. Go to the [Codio projects page](https://codio.com/home/projects).
    - See a "**Sign In**" screen? Use the "**Sign in via GitHub**" method like you did before (see Step #2 [here](#sign-up-for-a-codio-account)).

2. Click the "**DuckDuckHack**" project.

3. You should now see the three-pane window we previously saw. Press **Ctrl+Alt+R** (Cmd+Alt+R on a Mac), this will improve the layout a bit. (You can also click *View->Layouts->Default* from the command bar at the top).

4. Press **Shift+Alt+T** to open a new Terminal. (You can also click *Tools->Terminal* from the command bar at the top). You should see the right side pane change into a black command prompt.

5. Type **`git clone <Your GitHub URL Here>.git`** into the Terminal, replacing `<Your GitHub URL Here>` accordingly. It should look something like this for a Goodie:

    ```
    [04:30 PM codio@buffalo-pixel workspace {master}]$ git clone https://github.com/githubusername/zeroclickinfo-goodies.git
    ```
	
	Enter your Github credentials as prompted.

    _**If your Github password doesn't work**, you may need to enter a [Personal Access Token](https://github.com/settings/tokens) instead. Simply copy and paste your token from your [Github Settings](https://github.com/settings/tokens). (No worries - this happens if you have set up [Github's Two-Factor Authentication](https://github.com/blog/1614-two-factor-authentication) feature.)_

6. Press "**Enter**". You should see the Terminal print out some text that looks like this:

    ```
    [04:30 PM codio@buffalo-pixel workspace {master}]$ git clone https://github.com/githubusername/zeroclickinfo-goodies.git
    Cloning into 'zeroclickinfo-goodies'...
    remote: Counting objects: 18623, done.
    remote: Compressing objects: 100% (8083/8083), done.
    remote: Total 18623 (delta 8084), reused 18179 (delta 7868)
    Receiving objects: 100% (18623/18623), 5.50 MiB | 9.51 MiB/s, done.
    Resolving deltas: 100% (8084/8084), done.
    Checking connectivity... done.
    [04:30 PM codio@buffalo-pixel workspace {master}]$
    ```

7. The file tree on the left side of Codio should update. You'll see a new "**zeroclickinfo-xxxxx**" directory (where "**xxxxx**" is whichever Instant Answer type you chose: Goodie, Spice, Fathead, or Longtail).

8. Change the current directory of the terminal by typing **`cd zeroclickinfo-xxxxx`**, where "**xxxxx**" is whichever Instant Answer type you chose: Goodie, Spice, Fathead, or Longtail.

9. [Best practice, but not required] Create a new branch in your repository for this particular project. This lets you work on several contributions at one time - since you must create a separate branch for each contribution. 

	Create a new branch by typing  **`git checkout -b branch_name`**. You can use any branch name you like. You can switch between branches by using **`git checkout branch_name`**.
	
**Congrats!** You've now cloned the DuckDuckHack code onto your Codio machine. You're now prepared to code your first Instant Answer!

*If this is your first time using Git and GitHub, we've created an [overview of how you'll use Git](https://talsraviv.gitbooks.io/duckduckhackdocs/content/duckduckhack/resources/git-workflow.html) to contribute to DuckDuckHack.*

[![slack](https://talsraviv.gitbooks.io/duckduckhackdocs/content/duckduckhack/assets/slack.png) Have questions about git? Talk to us on Slack](mailto:QuackSlack@duckduckgo.com?subject=AddMe) or [email us](mailto:open@duckduckgo.com).