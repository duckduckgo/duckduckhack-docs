# How to Submit a Pull Request

The culmination of your contribution comes in the form of a pull request to the Github repository you forked. A pull request is your way of requesting that your contribution is merged back in to the main repository. Pull requests are a great, transparent way to review and discuss potential contributions.

The following are step-by-step instructions for submitting your changes as a pull request.

*If this is your first time using Git and GitHub, we've created an [overview of using Git](http://docs.duckduckhack.com/resources/git-workflow.html) to contribute to DuckDuckHack, which culminates in a Pull Request.*

## Committing Your Changes

The first step is to commit your changes to your local repository.

> If you've already done this, you can skip to [submitting a pull request](#submitting-a-pull-request), below.

Here is how to commit your code in the Codio environment:

1. Log in to [Codio](https://codio.com) and visit your [dashboard](https://codio.com/home/projects). (In the menu, click Codio > Dashboard)

2. Click on the **DuckDuckHack project**, which you previously forked and cloned.

3. Next, open a terminal window if it's not already open. (In the menu, click Tools > Terminal).

4. Enter the root directory of your forked Instant Answer repository. For example, for Goodies, enter the following into your terminal:

    ```shell
    cd zeroclickinfo-goodies
    ```

5. To add all new files to git, type **`git add .`**, then press enter.

    > This command tells the git repository to include and track changes to the files you've created. Even though the files were physically located in the repository, we need to explicitly tell git to track them.

5. We are now ready to finally commit the changes. Type **`git commit -m "Description of your changes"`** and press **`Enter`**. Git should print some text confirming the changes that have been committed.

    ```
    [04:35 PM codio@buffalo-pixel zeroclickinfo-goodies {master}]$ git commit -m "Description of your changes"
    [master 6aeb841] Description of your changes
     2 files changed, 56 insertions(+)
     create mode 100644 ...
     create mode 100644 ...
    ```

6. Now we'll upload the changes to *our* remote repository on GitHub. Once this step is done, we'll be ready to create a pull request back to the main, original DuckDuckGo repository.

	**If you are using multiple branches,** then type **`git push origin branch_name`** (where branch_name is the one you want to submit) and press **`Enter`**.

	**If you are working on the master branch alone,** simply type **`git push`** and press **`Enter`**. Enter your GitHub username and password, press **`Enter`** after each. Git will print some text to the Terminal letting you know that your code has been pushed to GitHub.

    ```
    [04:35 PM codio@buffalo-pixel zeroclickinfo-goodies {master}]$ git push
    Username for 'https://github.com': GitHubUsername
    Password for 'https://GitHubUsername@github.com':
    Counting objects: 75, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (60/60), done.
    Writing objects: 100% (75/75), 11.05 KiB | 0 bytes/s, done.
    Total 75 (delta 36), reused 0 (delta 0)
    To https://github.com/GitHubUsername/zeroclickinfo-goodies.git
       138f5bc..c69c517  master -> master
    ```


## Submitting a Pull Request

> Already experienced with pull requests? Make sure to paste your [Instant Answer Page URL](https://duckduckhack.com) in the description!

1. Open a **new browser tab** and go to your remote repository. For example, for Goodies: **`https://github.com/YOUR_GITHUB_USERNAME/zeroclickinfo-goodies`**.

2. Click the "**New pull request**" button (green button, middle of the screen).

    > Make sure you are on the correct branch where your changes are located!

3. Review the changes and click "**Create Pull Request**".

	> Make sure there's only **one** Instant Answer per pull request.

4. Enter a title for your pull request:

	If your IA is new, use the format: `"New {IA TOPIC} {IA TYPE}"`. For example:

	- "New Instagram Spice"
	- "New Firefox Cheat Sheet"

	If you're submitting a fix, use the title format: `"{IA NAME}: Brief explanation`. For example:

	- "PeopleInSpace: Use smaller local image, fallback to API when needed."

	Include the issue number in the description (conveniently, this will automatically resolve the issue upon merging). Describe your motivation, thought process, and solution in the description. For example:

	- "**Fixes #2038.** The images used by the API are very large and don't change often. I've but a smaller version of each image (and a 2x version for retina screens) in the share directory. The callback will try and load a local image based on the astronauts name and fallback to using the API's image if one does not exist."
	
5. Paste your **[Instant Answer Page URL](https://duck.co/ia/new_ia)** in the description field.

	> Our bot 'Dax' will automatically fill in the details from your IA page and additional information.

6. If you're submitting a fix, include **`Fixes #ISSUE"`** in the **description** as well (For example: "Fixes #3434").

	> Conveniently, Github will auto-close the issue when your pull request is merged.

6. Finally, click **"Create Pull Request"**!

> **IMPORTANT:** Don't worry if you get an initial error regarding failing Travis tests. The reason is that your IA page hasn't yet been moved out of the "Planning" status - which only community leaders/staff can do. As long as the ID in your IA page matches the ID in your code, and you've pasted the URL to your IA page, you can ignore this initial error.

Congratulations! A Community Leader or DDG staff member will review your contribution in turn.

Once your pull request is merged into the repository, it should be live on DuckDuckGo.com within a few days.

*Submitting a pull request is just the beginning. Learn about [keeping your IA awesome](http://docs.duckduckhack.com/maintaining/guidelines.html).*

