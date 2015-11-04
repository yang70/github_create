# GitHub Create

by [Matthew Yang](http://matthewgyang.com)

## Description
GitHub Create is a Ruby script that allows you to quickly create a remote repository on [github.com](https://github.com) and set it as the current project's `origin` all in one step from the command line.

It utilizes the [GitHub API](https://developer.github.com/v3/) along with the [Ruby Net::HTTP library](http://ruby-doc.org/stdlib-2.2.3/libdoc/net/http/rdoc/Net/HTTP.html) and [JSON module](http://ruby-doc.org/stdlib-2.2.3/libdoc/json/rdoc/JSON.html).

Once installed and configured, `cd` into your project's main directory and type:

```bash
$ ghcreate
```

This will create a GitHub repo with the same name as the current directory.  Optionally, you can pass a different name as an argument if you want:

```bash
$ ghcreate my-new-repo
```

Also, if Git has not been initialized in the directory it will run `git init` (will bypass if already being tracked by git).

Finally, it will run `git remote add origin` and set it to the newly created remote url (default is SSH, can be easily changed to HTTPS).

On success, it will print out a success message (don't worry about the `fatal` line, just means git wasn't initialized in the directory yet):

```bash
$ ghcreate
fatal: Not a git repository (or any of the parent directories): .git
Git initialized, GitHub repo 'example_repo' created! Remote origin set to git@github.com:exampleuser/example_repo.git
```
If there is an error (i.e.. the repo already exists on GitHub) it will print the message:

```bash
$ ghcreate
Error:  Validation Failed
name already exists on this account
```
## Installation / Configuration
### Create a new personal access token on GitHub
In order to access the GitHub API, we need an access token.

1. Sign in to your GitHub account
2. Navigate to `Settings`
3. On the left side menu, click on `Personal access tokens`
4. Click on `Generate new token`
5. Give the token a name (you can leave everything else to the default setting)
6. The token will be displayed

### Set the token as an environment variable
Copy down the access token and create an environment variable called `GITHUB_API`.  Here are a couple strategies for creating an environment variable:

* [For OS X](http://osxdaily.com/2015/07/28/set-enviornment-variables-mac-os-x/)
* [For Ubuntu](https://help.ubuntu.com/community/EnvironmentVariables)

### Create executable file

Add the `ghcreate` file from this repository to `usr/local/bin`.
Make it executable with the following command:

```bash
$ chmod +x /usr/local/bin/ghcreate
```

### Use HTTPS for remote instead of SSH
Changing to an HTTPS remote URL instead of an SSH url is easy, just modify the following line in the `ghcreate` code:

```ruby
remote = info['clone_url'] # changed from remote = info['ssh_url']
```

# Thanks!
Thanks for reading! Please [contact me](mailto:matt@matthewgyang.com) or open up a GitHub issue if you have any comments!
