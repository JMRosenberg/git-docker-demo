
# Git

## Get set up

There are a bunch of options for git hosts - this "app" is on GitHub, so let's start there. You'll learn as you go, really hands-on. The first thing to know: `git` is a wildly popular distributed version control system.

1. Make a [GitHub](http://github.com) account
2. Download and install [git](https://git-scm.com/downloads)
3. Configure your username and email
```
git config --global user.name "<your_user_name>"
git config --global user.email "<your_email>"
```
4. Set up ssh (for authentication with GitHub)
	1.  Check for existing keys at `~/.ssh/id_rsa` and `~/.ssh/id_rsa.pub`
	2. Assuming you don't have those, generate a new pair: `ssh-keygen -t rsa -C "your_email@example.com"`
	3. Copy the public key to your clipboard: `pbcopy < ~/.ssh/id_rsa.pub`
	4. Add it to your GitHub account
		1. In GitHub, open the top right menu, and select "Settings"
		2. Go to "SSH and GPG keys"
		3. "New SSH key"
		4. Name your key (recommendation: what you call your computer)
		5. Paste in the public key under "Key"
		6. "Add SSH key"
	5. Test with `ssh -T git@github.com` (you should see a message like "You've authenticated, but Github does not provide shell access."

## Learn the basics

### Cloning

Cloning a repository (repo) makes a local copy of a repo from a remote source.  This can be done over HTTPS or SSH, but since we just set up keys (because GitHub requires it) we'll use SSH.  That command looks like:
```
git clone git@github.com:JMRosenberg/git-docker-demo.git
```
Using HTTPS would look more like:
```
git clone https://github.com/JMRosenberg/git-docker-demo.git
```
Either way, you're pointing to the host (github.com) and then specifying the repo (JMRosenberg/git-docker-demo.git).

By default, this will create a folder in your current working directory, and name it after the repo (e.g. `git-docker-demo`).  If you want the files someplace else, just add a path onto the command (e.g. `git clone git@github.com:JMRosenberg/git-docker-demo.git ./folder-with-different-name`)

### Getting around

Try the following, see what they do!  Add `--help` after any of these to get the `man` page with additional information.

* `git status`
* `git log`
	* try adding `--graph`
* `git branch`
* `git diff`

### Making your first change

Before actually making a change, a quick diversion...

Pretty much every project of notable size (and lots of small ones too!) use branches as part of their workflow.  In short, branches are a way to split off sets of changes, so they can get developed independently without blocking other workstreams.  There are other benefits, but I'll probably just link to sources on them, because they mostly come into play at scale.

Mostly for the sake of learning, we're going to use branches!  I'm going with something similar to ["GitHub flow"](https://guides.github.com/introduction/flow/), because it's easy, and it gets the job done.  It's also what I use at my day job, and haven't found myself needing anything more complicated.

The default branch has historically been called `master`, which has some, uh, baggage.  Many projects are changing to something like `main` instead, although you can use absolutely anything you want!  This project still uses `master`, because I haven't changed it from the default (yet).

Before fully diving in, the rough plan:
* Make a new branch
* Switch to that branch
* Make a change
* Stage, commit, and push your code (more details later!)
* Open a Merge Request
* Merge it

By the end of this, you will have your own changes on the `master` branch of the repo, where whoever comes along next can build on it.

#### Create a new branch

1. Check which branch you're on with `git branch` - it should highlight `master`
2. Create a new branch with `git branch <unique-descriptive-name>`
3. You're still on `master` (confirm with `git branch` again), so switch to your new branch with `git checkout <unique-descriptive-name>`
4. Confirm you're on the new branch with one last `git branch`

**Pro tip:** Adding the `-b` flag to `git checkout` will create a new branch and switch to it all in one!  `git checkout -b <new-branch-name>`

#### Make a change

At the bottom of this file is a "Contributors" section.  Add your name to the list - you've earned it!

#### Commit your change

This change was small, so you're pretty confident it's correct.  But if you really want to make sure, `git status` will tell you there's a changed file.  It would also tell you if there were new/deleted/moved files.

`git diff` was empty before, but now will show you your change!  Make sure it looks good before continuing.

Now you can stage your changes with:
```
git add .
```
Note the `.` at the end - that adds _all changes_ from your working directory (recursively!).  You can be more selective if you want, specifying a file or folder to `add`.  Executing `git add` multiple times will stage the changes from all of the files you give it.  You can also see that the color of that file has changed when you run `git status`.  To remove a file that you accidentally added (without reverting your changes) you can use `git reset <file>`.



# Contributors
* Jake Rosenberg