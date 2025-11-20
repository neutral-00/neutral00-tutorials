# Initial Config

## Set Username And Email And Default Branch
```sh
git config --global user.name "your username"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
```

## Help On Global Config

```sh
git config -h # show the help content in the terminal
git help config # shows more detailed help content in the browser
```
- any other command help u can get with: git help `{command}`


## Why set user.email
- without it you can't do git push

Setting the user.email in Git global configuration is not mandatory, but it is recommended to do so. 
The user.email is used to associate your commits with your email address, which is useful for tracking changes and collaborating with others 
1. If you don’t set your email address, Git will prompt you to set it when you try to commit changes 
2. To set your email address globally, you can use the following command:
```sh
git config --global user.email "you@example.com"
```
This will set your email address for all repositories on your system that don’t have repository-specific values 
1. You can also set the email address for a specific repository by running the same command without the --global option 
from within the repository directory.

## See List Of Existing Global Configs
```sh
git config --list --global
```
## See All Git Configs And Their Source Files
```sh
git config --list --show-origin
```

## Remove A Global Config
```sh
git config --global --unset CONFIG_KEY
# example
git config --global --unset user.name
git config --global --unset user.email
```

## Edit Global Config
```sh
git config --global --edit
```

## Unset All Global Configs
```sh
git config --global --unset-all
```
if this doesn't work open your global git config in an editor say: vim ~/.gitconfig
and delete whichever line you want to reset.
