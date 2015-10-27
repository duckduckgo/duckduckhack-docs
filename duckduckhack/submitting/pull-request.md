# Submitting a Pull Request

The culmination of your contribution comes in the form of a pull request to the Github repository for your Instant Answer type. A pull request is a great, transparent way to review and discuss potential changes to a repository.

The following are step-by-step instructions for submitting your changes as a pull request.

## Committing Your Changes

The first step is to commit your changes to your local repository. *If you've already done this, you can skip to [submitting a pull request](#submitting-a-pull-request), below.* 

Here is how to commit your code in the Codio environment:

1. Log in to [Codio](https://codio.com) and visit your [dashboard](https://codio.com/home/projects). (In the menu, click Codio > Dashboard)

2. Click on the **DuckDuckHack project**, which you previously forked and cloned.

3. Next, open a terminal window if it's not already open. (In the menu, click Tools > Terminal).

4. Enter the root directory of your forked Instant Answer repository. For example, for Goodies, enter the following into your terminal:

    ```shell
    cd zeroclickinfo-goodies 
    ```

    Then press enter.

5. To add all new files to git, type **`git add .`**, then press enter.

    *This command tells the git repository to include and track changes to the files you've created. Even though the files were physically located in the repository, we need to explicitly tell git to track them.*
    
5. We are now ready to finally commit the changes. Type **`git commit -m "Description of your changes"`** and press **`Enter`**. Git should print some text confirming the changes that have been committed.

    ```
    [04:35 PM codio@buffalo-pixel zeroclickinfo-goodies {master}]$ git commit -m "Description of your changes"
    [master 6aeb841] Description of your changes
     2 files changed, 56 insertions(+)
     create mode 100644 ...
     create mode 100644 ...
    ```

6. Now we'll upload the changes to *our* remote repository on GitHub. Once this step is done, we'll be ready to create a pull request back to the main, original DuckDuckGo repository.

If you had created a branch for your current contribution then type **`git push origin branch_name`** and press **`Enter`**. If not type **`git push`** and press **`Enter`**. Enter your GitHub Username and password, press **`Enter`** after each. Git will print some text to the Terminal letting you know that your code has been pushed to GitHub.

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

*The steps below are all you need, but it's worth mentioning that GitHub provides [excellent instructions](https://help.github.com/articles/creating-a-pull-request) as well.*

1. Open a **new browser tab** and go to your remote repository. For example, for Goodies: **`https://github.com/YOUR_GITHUB_USERNAME/zeroclickinfo-goodies`**.

2. Click the "**Pull Request**" button (grey text, middle of the screen).

    For advanced users, make sure you are on the correct branch where your changes are located.

3. Review the changes and click "**Create Pull Request**".

	Make sure there's only **one** Instant Answer per pull request.

4. Enter a title for your pull request: 

	If your IA is new, use the format: "New {{IA NAME}} {{IA TYPE}}". For example:

	- "New Instagram Spice"
	- "New Firefox Cheat Sheet"
	- "New Color Hex Goodie"
	
	If you're submitting a fix, use the format: "{{IA NAME}}: Fixes {{ISSUE}}". For example:
	
	- "Forecast: Fixes #3434"
	- "Cheat Sheet: Fixes #4102"
	
	(Conveniently, this syntax will auto-close the Github issue when your pull request is merged.)

5. For new Instant Answers, copy the "Pull Request Template" for your type of Instant Answer from the links below. Paste it into the "Leave a Comment" text box, and answer the questions.

    - [Goodie Pull Request Template](https://raw.githubusercontent.com/duckduckgo/zeroclickinfo-goodies/master/pull_request_template_goodie.md)
    - [Spice Pull Request Template](https://raw.githubusercontent.com/duckduckgo/zeroclickinfo-spice/master/pull_request_template_spice.md)
    - [Fathead Pull Request Template](https://raw.githubusercontent.com/duckduckgo/zeroclickinfo-fathead/master/pull_request_template_fathead.md)
    - [Longtail Pull Request Template](https://raw.githubusercontent.com/duckduckgo/zeroclickinfo-longtail/master/pull_request_template_longtail.md) 

6. Add a screenshot of your Instant Answer to your answers:
	
	Go back to your Codio.com browser tab, and open the "Terminal" tab 
	
	Type `duckpan server`, then press enter.
	
	Click the DuckPAN Server button at the top of Codio, and type in a sample search query that will trigger your Instant Answer.
	
	Save a screenshot on your computer.

	Go back to your GitHub.com browser tab.

	Drag-and-Drop your screen shot into the textbox. The picture will be uploaded and a link will be generated.
	
7. Finally, click **"Create Pull Request"**!

Congratulations! A Community Leader or DDG staff member will review your contribution in turn.

Once your pull request is merged into the repository, it should be live on DuckDuckGo.com within a few days. Next, read about [maintaining your Instant Answer](#) over time.