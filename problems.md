# Problems along the road #

Here I will document problems I encountered and mistakes I made and how I solved them (Well, if I managed to)


* Px00		`fatal: repository 'https://github.com/S-Retr0/learning-git.com/' not found`

The problem is that I typed learning-git.com instead of learning-git.git when I was trying to connect to the remote repo (git remote add). My bad, this means that I was trying to connect to a non existing page. To solve the problem I just removed the remote connection and added the righ one.

	$ git remote -v
	origin	https://github.com/S-Retr0/learning-git.com (fetch)
	origin	https://github.com/S-Retr0/learning-git.com (push)
	$ git remote rm origin
	$ git remote -v
	$ git remote add origin https://github.com/S-Retr0/learning-git.git



* Px01		`remote: Invalid username or password.`

This time the problem was *two-factor authentication*. I had setup a yubikey for this account, and when I crated a new repo and tried to add it trough the terminal, it kept giving me the `remote: Invalid username or password.`
Once I removed the two-factor authentication, it worked. I should look at how I can use the yubikey in the terminal.


* Px02
