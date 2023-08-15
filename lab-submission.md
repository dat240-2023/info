# Instructions for Submitting a Lab Assignment to QuickFeed

## Note

This file describes the default way of setting up quickfeed. Since quickfeed as of this writing is currently under maintenance, then it is possible to clone the assignments repo first by navigating to a location you want to have the repo in the terminal and running the following commands:


```console
git clone https://github.com/dat240-2023/assignments
```

Then when you get access to your own repo then run the following commands in a terminal, when the path in the terminal is inside the folder with the .git folder inside:

```console
git remote set-url origin https://github.com/dat240-2023/{your_github_name}-labs
git remote set-url --push origin https://github.com/dat240-2023/{your_github_name}-labs
git remote add labs https://github.com/dat240-2023/assignments
```

Where you should replace {your_github_name} with the name of your github account, or just use the url provided in the repo.

By typing the command `git remote -v`, then it should look something like: 

```
origin  https://github.com/dat240-2023/{your_github_name}-labs (fetch)
origin  https://github.com/dat240-2023/{your_github_name}-labs (push)
labs https://github.com/dat240-2023/assignments (fetch)
labs https://github.com/dat240-2023/assignments (push)
```

This wil reconfigure your repository to point towards the labs repo by default. 

To pull changes from the assignment repo on updates:

```
git pull labs main
```

and to push to your labs repo:

```
git push origin main
```

## Setting up git repository

This section give step-by-step instructions on how to submit assignments.
In the following, you are expected to run commands from a terminal environment.

Here are two videos describing these steps: [Part 1 (~10 minutes)](https://youtu.be/Ewoax8goysg) and [Part 2 (~19 minutes)](https://youtu.be/rWrrrmgur4g).

- On macOS, Terminal can be started via Spotlight, by typing the first few letters of `terminal`.
- On Ubuntu Linux, you can click on the Activities item at the top left of the screen, then type the first few letters of `terminal`.
- On Windows, press start, and start typing `powershell`, or if you feel adventurous, you could try `Windows Terminal` or install it [here](https://www.microsoft.com/nb-no/p/windows-terminal/9n0dx20hk701)

1. Initially, you will get access to two repositories when you have signed up on QuickFeed.

   The first is the [`assignments`](https://github.com/dat240-2023/assignments) repository, which is where we publish all lab assignments, skeleton code and additional information.
   You only have read access to this repository, and its content may change throughout the semester, as we add new assignments or fix problems.

   The second is your own private repository named `username-labs`.
   You will have write access to this repository.
   Your solution to the assignments should be pushed here.

2. To get started, decide on a suitable location for your workspace for the course.
   In this guide we will use `$HOME/dat240-2023` as the workspace.
   Do the following making sure to replace `username` with your GitHub user name:

   Alternative 1 (preferred):
   (These steps requires that you have already set up your GitHub user with SSH keys.)

   ```console
   mkdir $HOME/dat240-2023
   cd $HOME/dat240-2023
   git clone git@github.com:dat240-2023/username-labs assignments
   cd assignments
   git remote add course-assignments git@github.com:dat240-2023/assignments
   git pull course-assignments main
   ```

   Alternative 2:
   (These steps will require that you type your GitHub password every time you access your GitHub repository.)

   ```console
   mkdir $HOME/dat240-2023
   cd $HOME/dat240-2023
   git clone https://github.com/dat240-2023/username-labs assignments
   cd assignments
   git remote add course-assignments https://github.com/dat240-2023/assignments
   git pull course-assignments main
   ```

3. You may be asked for username and password above.
    It is also possible to use ssh for GitHub authentication with password-less login. Some instructions can be found here: [steps](github-ssh.md).

4. One of the most useful git commands is: `git status`.
   This will most often be able to tell you what you should be doing with your working copy.

5. When working with git you typically iterate between the following steps:

    1. Edit files
    2. `git status` (check to see which files have changed)
    3. `git add <edited files>` (only add source files, not binaries)
    4. `git status` (check that all intended files have been added to the staging area)
    5. `git commit`
    6. `git status` (check that changes have been committed)

6. You may iterate over the steps in Step 5 many times.
   But eventually, you will want to push your changes to GitHub with the following command:

   ```console
   git push
   ```

   Note that this will only push your committed changes!

7. In summary, these are the typical steps that are necessary to make changes to
   files, add those changes to staging, commit changes and push changes to your
   own private repository on GitHub:

   ```console
   cd $HOME/dat240-2023/assignments/Lab1
   code program.cs
   # make your edits and save
   git add program.cs
   git commit
   # This will open an editor for you to write a commit message
   # Use for example "Implemented Assignment 1"
   git push
   ```

8. When you have pushed a change to GitHub, QuickFeed's built-in Continuous Integration system will pick up your code and run a set of tests against your code.

   Note that QuickFeed will only run tests against your master branch.
   If you do not want QuickFeed to test your code, you can create a separate branch,
   e.g. `featureX`, and work on that branch until you are finished. When you are ready
   to submit, simply merge the `featureX` branch into master and commit and push.
   QuickFeed will then pick up your code and run our tests on your code.

9.  You can check the output by going to the [QuickFeed web interface](http://uis.itest.run/).
   The results (scores and build log) should be available under the assignment's menu item.

11. If some of the QuickFeed tests fail, you may make changes to your code/answers as many times as you like up until the deadline.
    Changes after the deadline will count against the slip days.

## Final Submission of LabX

1. When you are finished with all the tasks for some `labX`, and you wish to submit,
   you may issue a commit message as follows to indicate that you are done:

   ```console
   git commit -m "username labX submission"
   ```

   The above text should be on the first line of the commit message, where `username` is your GitHub username and `X` with the lab number.

   If you have no changes to commit, then you can use:

   ```console
   git commit --allow-empty -m "username lab1 submission"
   ```

   If there are any issues you want us to pay attention to, please add those comments after an empty line in the commit message.
   If you later find a mistake and want to resubmit, please use `username labX resubmission` as the commit message.
   Note that these commit messages are not used by QuickFeed, they are only used to identify your lab submission commits when we do manual review.

   **Note:** Your slip days usage is calculated based on the deadline of `labX` and the time when you pushed the last commit to GitHub, that touched any of the files in the `labX` folder.

2. Push your changes to GitHub using:

   ```console
   git push
   ```

   After a while, you should be able to view your results in the QuickFeed web interface as described earlier.

## Update Local Working Copy from Course Assignments

1. As time goes by the teaching staff may publish updates to the
   course [assignments](https://github.com/dat240-2023/assignments) repo,
   e.g. new or updated lab assignments.
   First, check that your local working copy is clean using `git status`, which
   should instruct you to either commit your local changes or to restore any files
   whose changes you want to discard.

   Once your working copy is clean, you can fetch and integrate any updates from
   our course assignments repo into your working copy, with the following command:

   ```console
   git pull course-assignments master
   ```

2. If there are conflicting changes, you will need to edit the files with conflicts.
   Normally, the conflicts are relatively straight forward to fix by picking one of
   the two changes: (i) your local change, or (2) the course assignment change.
   Sometimes you need to merge the two changes, if both are relevant for your code.
   Remember to remove the lines that start with `>>>>`, `====`, and `<<<<<`.
   This is necessary to commit your changes, once the conflict has been resolved.

## Updating Local Working Copy with Changes from Web Interface

1. If you make changes to your own `username-labs` repository using the GitHub
   web interface, and you want to pull or fetch those changes to your local computer's
   working copy, you can run the following command:

   ```console
   git pull
   ```

   Or (depending on which merge strategy you prefer)

   ```console
   git fetch
   git rebase
   ```

2. If there are conflicting changes, you will need to edit the files with conflicts.
   Normally, the conflicts are relatively straight forward to fix by picking one of
   the two changes: (i) your local change, or (2) the course assignment change.
   Sometimes you need to merge the two changes, if both are relevant for your code.
   Remember to remove the lines that start with `>>>>`, `====`, and `<<<<<`.
   This is necessary to commit your changes, once the conflict has been resolved.

## Working with Group Assignments

To work on group assignments, you need to clone your group's repository to your own machine, and pull the `assignments` repository into the group's repository.
In the instructions below, replace `groupname` with your group's repository name.
We assume you have already created the `dat240-2023` directory on your machine.

```console
cd $HOME/dat240-2023
git clone git@github.com:dat240-2023/groupname.git
cd groupname
git remote add course-assignments git@github.com:dat240-2023/assignments
git pull course-assignments master
```

All group members will have write access to the `groupname` repository, and it is this repository that your solutions should be pushed to.
QuickFeed will run our tests against your `groupname` repository.

Remember that you should run:

```console
git pull course-assignments master
```

Every once in a while, to check if we have posted updates to the assignments, including new assignments.

Read the next section, for instructions on pulling in changes from your group partners.

## Updating Local Working Copy with Changes from Other Group Members

1. If another group member has made changes that has been pushed to GitHub,
   and you want to pull or fetch those changes to your local computer's
   working copy, you can run the following commands:

   ```console
   git pull
   ```

   Or (depending on which merge strategy you prefer)

   ```console
   git fetch
   git rebase
   ```

2. If there are conflicting changes, you will need to edit the files with conflicts.
   Normally, the conflicts are relatively straight forward to fix by picking one of
   the two changes: (i) your local change, or (2) the course assignment change.
   Sometimes you need to merge the two changes, if both are relevant for your code.
   Remember to remove the lines that start with `>>>>`, `====`, and `<<<<<`.
   This is necessary to commit your changes, once the conflict has been resolved.