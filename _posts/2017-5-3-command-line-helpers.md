---
layout: post
title: understanding the command line
---

# Understanding the Command Line
#coding

**NAVIGATION**

Get the current directory’s path.

`pwd`

List the files in the current directory.

`ls`

List hidden files in current directory.

`ls -la`

Change directory.

`cd                    # exits to the root directory`
`cd ‘NameOfDirectory’  # changes to the specified directory`
`cd ..                 # backs out of the current directory`

Make directory.

`mkdir ‘NameOfDirectory’ # creates a directory with the given name within the current scope`

Print contents of file inline.

`cat path/to/file`

View a file.

`less path/to/file`

Edit a file with nano.

`nano path/to/file`

Move a file.

`mv path/to/file new/path/to/file`

- - -
**GIT**

Check which files have been changed in the directory.

`git status`

Pull remote changes on a branch.

`git pull`

Add current changes to next commit.

`git add -A`

Commit added changes to local .git repository.

`git commit -m "some message about commit"`

Push changes to remote repository.

`git push`

See changes by file.

`git diff`

Removed tracked files after being added to .gitignore.

`git rm -r --cached .`
`git add .`
`git commit -m "removed untracked files"`

Return list of local branches.

`git branch`

Checkout a local branch.

`git checkout branch-name`

Create a new branch **!TIP! - This will include your uncommitted changes**.

`git checkout -b branch-name`  

Checkout a file from another branch.

`git checkout branch-name -- file-name`

Stash your current changes to apply later or on a different branch.

`git stash`

Apply last set of stashed changes for the current branch.

`git stash apply`

Apply last set of stashed changes to the current branch.

`git stash pop`

Edit your commit history.

`git rebase -i HEAD~<number-of-commits-to-rebase>`

Delete any current changes to the directory.

`git reset --hard`

Reset directory to match alternate branch (VERY DESTRUCTIVE):

`git reset --hard branch-name`

Reset you last commit.

`git reset HEAD~`

- - -
**!!!TIP!!!**
First install Sublime text editor. (https://www.sublimetext.com/) Aliases work equally with other programs.
Then alias Sublime text editor by adding this to your .bash_profile.

`alias sublime="open -a /Applications/Sublime\ Text\.app"`


Call this to make the changes affect your current terminal session.

`source ~/.bash_profile`


Then call your new command to open the user level directory in sublime. I have my .bash_profile open here showing my alias for Sublime along with an alias for Xcode.

`sublime ~/`


This will show all of your local system files and folders that even finder wont show including your profiles.
<a href='bash-alias-example'>bash-alias-example</a>

- - -
**BASH**

Switch from alternate cli.

`exec bash`


Profile.

`~/.bash_profile`


- - -
**ZSH**

Switch from alternate cli.

`exec zsh`


Profile.

`~/.zshrc`


- - -
**APT**

Check list of installed packages via apt-get.

`apt list -—installed`


- - -
**GENERATING PUBLIC/PRIVATE RSA KEY PAIR**

Generate private key.

`openssl genrsa -aes256 -out .private-key.pem 2048`

1. You will be prompted for a password. (Must be at least 4 digits)

2. You will be prompted for the same password.

Remove the password from the key.

`openssl rsa -in .private-key.pem -out .private-key.pem`

1. You will be prompted for the password.

Generate public key.

`openssl rsa -in .private-key.pem -pubout -out .public-key.pem`

- - -
**Curl**

**Common Options**

Make curl display a simple progress bar instead of the more informational standard meter.

`-#, --progress-bar`

Supply cookie with request. If no `=`, then specifies the cookie file to use (see `-c`).

`-b, --cookie <name=data>`

File to save response cookies to.

`-c, --cookie-jar <file name>`

Send specified data in POST request. Details provided below.

`-d, --data <data>`

Fail silently (don't output HTML error form if returned).

`-f, --fail`

Submit form data.

`-F, --form <name=content>`

Headers to supply with request.

`-H, --header <header>`

Include HTTP headers in the output.

`-i, --include`

Fetch headers only.

`-I, --head`

Allow insecure connections to succeed.

`-k, --insecure`

Follow redirects.

`-L, --location`

Write output to <file>. Can use `--create-dirs` in conjunction with this to create any directories specified in the `-o` path.

`-o, --output <file>`

Write output to file named like the remote file (only writes to current directory).

`-O, --remote-name`

Silent (quiet) mode. Use with `-S` to force it to show errors.

`-s, --silent`

Provide more information (useful for debugging).

`-v, --verbose`

Make curl display information on stdout after a completed transfer. See man page for more details on available variables. Convenient way to force curl to append a newline to output: `-w "\n"` (can add to `~/.curlrc`).

`-w, --write-out <format>`

The request method to use.

`-X, --request`

**POST**

When sending data via a POST or PUT request, two common formats (specified via the `Content-Type` header) are:
	* `application/json`
	* `application/x-www-form-urlencoded`

Many APIs will accept both formats, so if you're using `curl` at the command line, it can be a bit easier to use the form urlencoded format instead of json because
	* the json format requires a bunch of extra quoting
	* curl will send form urlencoded by default, so for json the `Content-Type` header must be explicitly set

For sending data with POST and PUT requests, these are common `curl` options:

1. `request type`
	* `-X POST`
	* `-X PUT`

2. `content type header`
	* `-H "Content-Type: application/x-www-form-urlencoded"`
	* `-H "Content-Type: application/json"`

3. `data`
	* form urlencoded: `-d "param1=value1&param2=value2"` or `-d @data.txt`
	* json: `-d '{"key1":"value1", "key2":"value2"}'` or `-d @data.json`

**Examples**

1. POST application/x-www-form-urlencoded

`application/x-www-form-urlencoded` is the default:

Ex:  `curl -d "param1=value1&param2=value2" -X POST http://localhost:3000/data`

explicit:

`curl -d "param1=value1&param2=value2" -H "Content-Type: application/x-www-form-urlencoded" -X POST http://localhost:3000/data`

with a data file

`curl -d "@data.txt" -X POST http://localhost:3000/data`


2. POST application/json

Ex: `curl -d '{"key1":"value1", "key2":"value2"}' -H "Content-Type: application/json" -X POST http://localhost:3000/data`

with a data file

`curl -d "@data.json" -X POST http://localhost:3000/data`

- - -
**Web**

Find PID of running tcp connection.

`sudo lsof -I tcp:[PORT]`

Kill running tcp connection.

`kill [PID]`

- - -
**Docker**

Creating a `Dockerfile`.
	- [ ] [Udacity](https://classroom.udacity.com/courses/ud1031/lessons/a4f1bbd1-144a-4716-b80e-2ba23492f892/concepts/e4c74e80-9eee-4498-b8f4-3bebafc0e623)

Build your Docker image.

`docker build -t swift-nano:1.0.0 .`

	- [ ] Specifying `-t` lets you set a tag `swift-nano:1.0.0`  and builds the docker image at the specified path `.`

Run an already built Docker image.

`docker run -it --privileged swift-nano:1.0.0 /bin/bash`

	- [ ] Specifying `-it` opens the `/bin/bash` shell in the newly created container.

List all compiled Docker images.

`docker images`

See all currently running Docker images.

`docker ps`

Connect to a running Docker container.

`docker attach [OPTIONS] CONTAINER`

Stop a Docker container.

`docker stop CONTAINER ID`

Remove a Docker container.

`docker rm CONTAINER ID`

- - -
**Swift**

Create a swift package from an empty directory.

`swift package init --type executable`

- - -
