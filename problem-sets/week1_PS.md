# Week 1 Problem Set


This week’s in-class activity and problem set will be a little different
than usual! We’ll (unfortunately) be starting with one of the most
difficult aspects of a reproducible workflow… **getting RStudio and
GitHub to talk to each other.** Luckily, this initial setup is a one
time process, so you won’t need to do this again!

We will be working through this together in class, but it’s possible
(*perhaps likely*) that we won’t get all the way through. If you’re
encountering difficulties, I have included some links on
[Troubleshooting](https://github.com/stepfanie-aguillon/eeb201-R-course/blob/main/problem-sets/week1_PS.md#troubleshooting)
at the end.

**For this assignment, your goal is to work through this entire process
and complete your first two “commits” on GitHub.**

**Deadline**: 10/8/25 10pm

## Why use GitHub?

GitHub is a great tool for Open Science! But it’s also a great tool for
your *own* analysis workflow! Hopefully you learned about the basics of
GitHub in the [pre-class reading](https://stat545.com/r-basics.html).

Have you ever had a file history that looks like this?

<img src="./PS-images/week1/final_doc.png" style="width:50.0%"
alt="PhD Comics" />

Version control in GitHub keeps all of these changes tidy and in one
place using “commits”! So you’re able to easily track changes and know
what file is the most up-to-date.

## Creating your course repo in GitHub

You should have already made a GitHub account and installed Git on your
computer, but if not, please follow directions in the [installation
guide](https://github.com/stepfanie-aguillon/eeb201-R-course/blob/main/install-guide.md#step-4-github).

Rather than working directly in a repository (“repo”) in your own
personal account, we will be using the functionality built into GitHub
Classroom to create a repo that Stepfanie has shared access to. You will
use this shared repo to submit your problem sets throughout the quarter.

### To begin your shared repo, click [this link](https://classroom.github.com/a/Owatds-K).

Once you’ve created your course repo, you should notice that it’s hosted
within the course’s organization rather than your personal GitHub
account. **You should star this repo, so it will show up within your
personal account.**

![GitHub screenshot](./PS-images/week1/course-repo-creation1.png)

Once you’ve starred the repo, you can find it again by clicking on
“Stars” on the profile page of your GitHub account.

![GitHub screenshot](./PS-images/week1/course-repo-creation2.png)

## Connecting your local machine to GitHub

We first need to make sure your installation of Git can talk directly
with GitHub. There are [many ways](https://happygitwithr.com/hello-git)
to do this, but in this class we will use the R Package `usethis`. First
we will need to install the package using the `install.packages()`
command.

``` r
install.packages("usethis")
```

You will now have this package installed, but you need to “load” it. To
load a package in R we use the `library()` command. Note that you only
need to *install* a package once, but you will need to *load* it each
time you open R.

``` r
library(usethis)
```

We will use the `use_git_config()` command within the `usethis` package
to connect Git and GitHub. You will need to enter the username and email
address associated with *your* GitHub account.

``` r
use_git_config(user.name = "Josie Bruin", user.email = "josie.bruin@ucla.edu")
```

Finally, to allow you to have full functionality using GitHub you will
need to generate a [personal access
token](https://happygitwithr.com/https-pat#https-pat), as your password
alone is not enough. We will use the `create_github_token()` command
within the `usethis` package.

``` r
create_github_token()
```

This will open a GitHub window in your browser and you will be required
to enter a password and/or two-factor authentication.

Enter a descriptor for this token in the “Note” section, change the
expiration date to 1/1/26, and then make sure `repo`, `workflow`,
`gist`, and `user` are selected. Finally, **click the green button at
the bottom** to generate your token. Keep this GitHub page open for now.

<img src="./PS-images/week1/PAT1.png" style="width:75.0%"
alt="Personal access token screenshot" />

Now, store this personal access token. Use the following code and paste
in your personal access token as the response.

``` r
gitcreds::gitcreds_set()
```

You should get a result that looks like this:

``` r
? Enter password or token: ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
-> Adding new credentials...
-> Removing credentials from cache...
-> Done.
```

## Connecting RStudio and your course GitHub repo

Once Git, GitHub, and RStudio are all set up and talking to each other,
you are ready to connect your individual course repo to your local
machine!

### Copy the GitHub repo address

Next, you will need to **copy the repo address** from GitHub using the
green “code” button. You will want to copy the **HTTPS** option.

<img src="./PS-images/week1/repo-clone.png" style="width:75.0%"
alt="GitHub screenshot" />

### Create a new R Project in RStudio

We will return to RStudio for the next steps. You will create a new
RStudio Project: File \> New Project

![RStudio screenshot](./PS-images/week1/rproject1.png)

For the next two menu windows, **select “Version Control” and then
“Git”**

![RStudio screenshot](./PS-images/week1/rproject2.png) ![RStudio
screenshot](./PS-images/week1/rproject3.png)

### Connect your GitHub repo to this RProject

We’re now ready to connect your RProject with the GitHub repo!

- Paste the repo address you copied from GitHub into the “Repository
  URL” field.

- Press tab to autofill your “Project directory name” so that it matches
  the repo name on GitHub. (Note that your repo will be named slightly
  differently than what’s shown in the screenshot)

- Browse to your desktop.

- Click “Create Project.”

![RStudio screenshot](./PS-images/week1/rproject4.png)

Once completed, this repository is going to be a folder on your local
computer and your RStudio window should boot up with your new R Project!

Your RStudio should now show a “Git” tab within the upper right panel
**and** that you’re working within a new R Project (found right above
the upper right panel). Again, the name of your R project will be
slightly different from what’s shown in the screenshot below.

![RStudio screenshot](./PS-images/week1/rproject5.png)

## Completing your first commit (or two!)

### Syncing your RStudio changes to GitHub

There are 4 steps to syncing your local RStudio changes with your GitHub
repository. We’re going to walk through these one by one.

![RStudio screenshot](./PS-images/week1/pull-push-schematic.png)

### Pull

We will start by “pulling” from our GitHub repository. Because the
repository is new, the “local” version (the one on your computer) should
be the same as the “remote” version (the one on GitHub). But to get into
the good habit of pulling often, we will do this first.

To pull from GitHub, click the blue “pull” arrow in the Git panel.

![RStudio screenshot](./PS-images/week1/pull1.png)

Once you do this, you should see a message box that looks like this:

![RStudio screenshot](./PS-images/week1/pull2.png)

### Editing the README file

Within your new R Project folder, you will find a file named
`README.md`. This is the file that creates the “homepage” of your
repository (the page you see when you first open a GitHub repo). You
should see that there is already some information included that matches
what is shown on the GitHub repo online.

**Let’s edit this file to see how GitHub tracks our changes.**

Open the file in RStudio (you may need to drag and drop the file into
RStudio or right click \> open with \> RStudio) and edit the text below.
Replace `enter your name here` with your name and save the file.

``` r
Student: enter your name here
```

**Notice that the `README.md` file in the Git panel has changed to a
blue “M”.** (This means the file has been modified… And that GitHub is
already tracking it! Great!) We’ll talk more about what these letters
mean shortly.

### Stage

Next, we will stage the files we want to commit. Click the “Staged”
boxes next to each of the files in the Git panel. You will see that the
“Status” changes from a yellow “?” or blue “M” to a green “A”.

![RStudio screenshot](./PS-images/week1/staging1.png)

Here are what the different stage statuses mean:

![RStudio screenshot](./PS-images/week1/staging2.png)

### Commit

Next, we will start our “commit” by clicking the “Commit” option in the
Git panel.

![RStudio screenshot](./PS-images/week1/commit1.png)

This will open the commit dialogue window where we will need to write a
“commit message” and then click the “commit” button. (Note that the
files included in your commit will be different from those shown in the
screenshot.)

<img src="./PS-images/week1/commit2.png" style="width:75.0%"
alt="RStudio screenshot" />

This will give you a pop-up message that should indicate that the commit
has “worked”! (And not have any errors… If you are encountering errors
at this stage, then there may be an issue with your GitHub/Git/RStudio
connection that will require
[Troubleshooting](https://github.com/stepfanie-aguillon/eeb201-R-course/blob/main/problem-sets/week1_PS.md#troubleshooting)!)

<img src="./PS-images/week1/commit3.png" style="width:75.0%"
alt="RStudio screenshot" />

**Note that committing is different from saving a file! So don’t forget
to save your files along the way too!**

### Push

Now, we’re ready for the final step and we will “push” our changes to
our GitHub repository. From either the Git panel or the commit window
press the green “Push” arrow.

![RStudio screenshot](./PS-images/week1/push.png)

**CONGRATS! You’ve done it!!**

Refresh GitHub in your browser and you should now see these updates
reflected in your GitHub repository online!

### Try it again with your script from class!

Move the script you saved from our practice in class into the
`problem_sets` folder within your RProject. You should now see this new
file included in the list of files in your Git panel. Do you?

Practice your four step pull \> stage \> commit \> push process to add
this R script to your GitHub repository. Make your commit message
`"this is my first independent commit!"`

<img src="./PS-images/week1/push-pull-allisonhorst.png"
style="width:50.0%" alt="Artwork by Allison Horst" />

How does this script look on GitHub? Inspect the [commits
history](https://docs.github.com/en/pull-requests/committing-changes-to-your-project/viewing-and-comparing-commits/differences-between-commit-views)
of your new repository.

## Troubleshooting

Getting RStudio and GitHub connected for the first time can be
**really** complicated! It is possible that you will run into
difficulties somewhere along the line in getting this setup! Here are
some resources for beginning to troubleshoot:

- Happy Git with R [Chapter
  13](https://happygitwithr.com/rstudio-see-git)

- Happy Git with R [Chapter
  14](https://happygitwithr.com/troubleshooting)

- If you want some videos going through this process: [R For The Rest of
  Us](https://rfortherestofus.com/2021/02/how-to-use-git-github-with-r)

If you’re still having difficulties, **come to office hours** or Slack
me to set up a meeting!
