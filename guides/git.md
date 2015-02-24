# Git

## Commit
When it comes to committing stuff, there are two important principles to follow. These are:

### Organise your commits

**Small, logical commits are much more useful** than big ones that contain a bunch of unrelated changes.

Ideally, **a single commit should correspond to a single feature or piece of functionality**, or at most a few small changes that are logically related (eg. styling of a single section or page). This makes it easier to understand the history and make use of other git tools like `revert`

If you've been working on more than one thing, avoid the temptation to just `git add .` and commit. Instead use `git diff` to remind yourself of what you've done, and selectively `git add` changes that logically go together. This ability to retrospectively package stuff up into separate commits (via `git add`) is one of the major advantages that Git has over earlier version control systems.

If you've made unrelated changes to the same file, you can stage them separately using `git add --patch` (or `git add -p` for short). This identifies separate 'hunks' within the file that have been changed, and will step through, allowing you to select which ones you'd like to  stage.

**Suggestion:** Although the command line is generally preferable for most things, committing is one place where you might find a GUI useful. There are various GUIs available, but Git comes with a basic one that you can open by typing `git gui`. This gives you an overview of your modified files and makes it easy to stage / unstage them (and select individual lines and hunks to stage too).

### Write nice commit messages

:(  
~~`git commit -m "Fixed some bits and pieces with the graph"`~~

:)  
`git commit -m "JS: added a 'drawGraph' function"`  
`git commit -m "JS: fixed bug where 'drawGraph' messed up negative values"`  
`git commit -m "Styles: tweaked the colour palette"`  

Avoid the temptation to write commit messages like **"Did a bunch of stuff"** or **"Various things on the homepage and about page"**. Having good commit messages is like having well-commented code: a `git log` full of clear messages makes it much easier for others, or your future self, to see what happened when, and why.

**Recommendation:** Prefix your commit messages with a single word that describes the area that your commit most closely relates to. (eg. "JS: " for Javascript /  "Styles: " / "Homepage: " / "About: "). This isn't essential, but it's a useful convention because it makes it easier to search the history for commits relating to a particular area (eg. searching for "About" would allow you to filter down to commits that involved updates to the "about" section). It also makes it easier to quickly skim-read the history when you do `git log --oneline`.

In addition to the above, here are a few more guidelines for commits:

### Commit often

Git's staging means you can pile up a load of changes and commit them later. That's fine, but it's less work to commit stuff as you go along. It also makes it easier to make sure that your commits are neatly separated out, and allows you to try stuff out quickly and `git checkout -- .` to get back to the last commit if it doesn't work out.

### Avoid committing unnecessary files

Think carefully before adding, eg. large asset files to the repo. If they don't really need to be in the repo, .gitignore them.

### Close issues in commit messages

BitBucket and Github both let you mark an issue in the issue tracker as resolved by referring to it in the commit message. This is a good way to close an issue because it explicitly links the closed issue with the commit that fixed it.

To resolve an issue via a commit message, just put something like `(resolves #36)` or `(fixes #12)` at the end of the message. More details [here](https://confluence.atlassian.com/display/BITBUCKET/Resolve+issues+automatically+when+users+push+code).

## Branch

### Don't develop on the master branch

Work in progress should be on a local feature/development branch. Always pull changes to master, then branch (or merge the latest changes into your feature branch) and work on your feature branch. (eg. `git pull origin master` --> `git branch feature/graph` --> `git checkout feature/graph`). This means that it's always possible to put the thing you're working on to one side: if, eg. an urgent bug comes up, you can just checkout master again, and 

The name of your feature branch doesn't matter too much. The main thing is to avoid naming clashes with existing branches. A good convention is to use `feature/` as a prefix for feature branches and `bugfix/` as a prefix for bug fix branches.

On larger projects, when pushing code back out, instead of merging into master, push your feature branch to the main repo and issue a pull request on Bitbucket so someone else can cast a fresh eye over your changes before merging them into the master branch.

Our workflow should look something like this:

- **pull** from remote master
- **branch** locally, and develop on feature branch
- **push** to remote feature branch
- When your remote feature branch is ready for merging, issue a pull request on Bitbucket
- **merge** feature branch into master (someone else does this)

We can be pragmatic about the pull request stage. In principle, it would be great for all code to get reviewed this way, but in practice - especially for smaller projects, or minor changes - sometimes this step might get in the way. If it does, it's ok to just merge the feature into master yourself. Basically, issue pull requests where possible, but do the merge if you're confident about it, or if the pull request process is going to cause a bottleneck.

The aim of all this is to keep the quality of code in the `master` branch as high as possible.

## Blame

If there's a piece of code that you don't understand or have questions about, `git blame <filename>` is a useful way of finding out who introduced it, and when (it gives you a line-by-line breakdown of who wrote each line, and which commit the line was introduced in). This makes it easier to find out why something non-obvious is the way it is - either by checking the relevant commit message, or asking the person in question.
