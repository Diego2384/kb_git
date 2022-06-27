# book_2022_fluent_python

# Git Config

The Git configuration file contains a number of variables that affect the Git commands’ behavior. We can change the values of these variables using commands or by editing the git config file.

Git divides configuration options into three separate files:

- Local: For individual repositories ~ /.git/config
    - `git config --local <property> <value>`
    - *The global config file in Windows is under **git-repo\\.git\config***
- Global: For User-specific settings ~ /.gitconfig
    - `git config --global <property> <value>`
    - *The global config file in Windows is under **C:\Users\\username\\.gitconfig***
- System: For system-wide settings ~ $(prefix)/etc/gitconfig
    - `git config --system <property> <value>`
    - *The system config file in Windows is under **C:\ProgramData\Git\config***


To show the config content:

`git config --list --show-origin --show-scope`

## Add multiple identities

Let’s consider a case, on one machine you may contribute to git repositories using different identities (e.g. some for your company works, some for your personal projects). You can set up your git config file to set your identity based on the directory you’re currently in, instead of always worrying about which email/name you’re trying to push to remote with and having to change it manually here and there.

Now, we will make some changes to the global configuration file and will also create some new configuration files in the same directory where your global configuration file resides.

For Mac, you can use this command to create a new file named gitconfig_github ( you can use another name as per your choice ) $ touch ~/.gitconfig_company

For windows, you can create a new file in the same directory of your global config file and name it gitconfig_company ( you can use another name as per your choice ).

Now add the following settings to this file and save the file. These settings will be used for your company work directory, so you can use your company identities.

```
[user]
   email = company_email@xyz.com
   name = Diego Gasco
```

Next, create another file as per the same instruction with a different name, I will use gitconfig_diego , and add the following settings in this file and save it. These settings will be used for your personal projects’ identities.

```
[user]
   email = personal_email@gmail.com
   name = Diego Gasco
```

Now, you have two different identities created, we will specify both in our global configuration file. Add the following settings in your global configuration file underneath the [user] settings, and save the file.

```
[includeIf "gitdir:*/CompanyDirectory/"]        
   path = ~/.gitconfig_company 
[includeIf "gitdir:*/Diego/"] 
   path = ~/.gitconfig_diego
```

Let me explain these settings. For the projects residing in the directory named ‘CompanyDirectory’, Git will use the [user] settings from the /.gitconfig_company file, which will be your company projects generally. In another case, all the projects belong to the directory named ‘Diego’, Git will use the [user] settings from the /.gitconfig_diego file.


## Git Config for using VS Code as default editor

Here we have the commands to configure some settings to use VS Code as default editor for Git:

`git config --global core.editor "code --wait --new-window"`

`git config --global diff.tool vscode`
`git config --global difftool.vscode.cmd 'code --wait --diff $LOCAL $REMOTE'`

`git config --global merge.tool vscode`
`git config --global mergetool.vscode.cmd 'code --wait $MERGED'`


Any of this configurations may be unsetted with: 

`git config --global --unset <property>`

After excute this commands, the ~/.gitconfig file contains something like this lines: 


```
$ cat ~/.gitconfig
...
[merge]
	tool = vscode
[core]
	editor = code --wait --new-window
[difftool "vscode"]
	cmd = code --wait --diff $LOCAL $REMOTE
[diff]
	tool = vscode
[mergetool "vscode"]
	cmd = code --wait $MERGED
...
```

## Git Config for pruning during fetch

 Pruning during fetch is a cleanup method that deletes outdated remote references in your .git directory when you do a git fetch --prune.
 
 This can be automated with a setting in Git configuration:

`git config --global fetch.prune true`

*(**No funciona** por comando)*

This is reflected in the git config file with this entry:

```
[fetch]
    prune = true
```

## Git Config for setting the default branch

When initializing a repository (git init), the default branch is master. Today, some developers would prefer that to be main or something else entirely.

You don't have to create a new branch called main, delete the master branch, and use the main as your default. That's a long process. In the Git configuration file, you can set a default branch upon Git initialization. Here's how:


`git config --global init.defaultBranch main`

*(**No funciona** por comando)*

This is reflected in the git config file with this entry:

```
[init]
    defaultBranch = main
```

## Git Config for shorting git status

When we type `git status` we obtain a long desription of the status; if we want to get it summarized, we can execute:

`git config --global status.short true`

*(**No funciona** por comando)*

This is reflected in the git config file with this entry:

```
[status]
    short = true
```