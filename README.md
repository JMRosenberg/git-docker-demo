
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
