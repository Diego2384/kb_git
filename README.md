# book_2022_fluent_python

# Git Config

Here we have the commands to configure some settings to use VS Code as default editor for Git:

`git config --global core.editor "code --wait --new-window"`

`git config --global diff.tool vscode`
`git config --global difftool.vscode.cmd 'code --wait --diff $LOCAL $REMOTE'`

`git config --global merge.tool vscode`
`git config --global mergetool.vscode.cmd 'code --wait $MERGED'`


Any of this configurations may be unsetted with: 

`git config --global --unset <property>`

After excute this commands, the ~/.gitconfig file contains something like this lines: 


`$ cat ~/.gitconfig
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
`
