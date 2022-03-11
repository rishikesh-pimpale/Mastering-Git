<details>
<summary>Git Essentials</summary>

## Basics

Version | -
--|--
`git --version`	| check installed version of git
`git update-git-for-windows`	| windows
`which git` | mac 

<br/>

**Basic Git configuration** | -
--|--
`git config --system` | System - applies to all users (Program Files\Git\etc\gitconfig)
`git config --global`	| User - can override System (User\.gitconfig)
`git config`	|	Project - project specific (project\.gitconfig)
`git config --global user.name` | get config 
`git config --global user.email "rishikesh_pimpale@redmane.com"`	|	set config
`git config --list` |	list all configurations
`git config --global core.editor	"atom --wait"` | Set to Notepad++ or Atom
`git config --global color.ui true`		| set to true
`git config --global core.excludesfile <filename>` | global ignore file

<br/>

**Git help** | -
--|--
`git help log` | learn more about log

<br/>

**Getting Started** | -
--|--
`git init` | Initialize current project/folder to be a git repository. (Explore .git directory for config. HEAD pointes to refs/head/master)
`git add .`	 | add all untracked files to staging index
`git commit -m <commit_message>`	|	commit changes to repository with a message	
`git commit --all` | commits all changes to tracked files directly to repo
`git commit -a` | shorthand. This opens editor for message with multiline description 
`git commit -am <commit_message>`	| shorthand to commit with message 

<br/>

**Best practices for commit messages**
- Single Line Summary (less than 50 characters), optionally followed by a blank line and a more complete description. Keep each line to less than 72 characters.
- Write commit messages in present tense.
- Bullet points are usually asterisk or hyphens.
- Be clear and descriptive
- Use atomic commits

<br/>

**Git Log** returns a log of all commits with the latest commit on top

`git commit -m "Initial Commit"` 

`git log` 
 
```git
commit 32asdf654asdf21asdf21asdf64aasd56fasd65f (HEAD > master)
Author: Rishikesh Pimpale <rishikesh_pimpale@redmane.com>
Date: Sun Apr 25 07:45:00 2020 -0500
Initial Commit
```

Git Log | -
--|--
`git log` | use Q to exit and space for pagination or F/B 
`git log --oneline` | one line logs with commit message
`git log -n 5` | limit logs to last 5 commits
`git log -5` | shorthand
`git log --since=2020-01-01`  | `since` ,  `after`,  `until`, `before`  (since="3 days ago")
`git log --author="Rishi"` | filter by author name
`git log --grep=<commit message>`	| search by meta data (global regular expression)
`git log <commit1>..<commit2>	`	| limit results between 2 commits
`git log <path/fileName>` | see history of changes

<br/>

**Create a new repository on the command line**
```git
echo "# PICO-CSS" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/rishikesh-pimpale/PICO-CSS.git
git push -u origin main
```
**Push an existing repository from the command line**
```git
git remote add origin https://github.com/rishikesh-pimpale/PICO-CSS.git
git branch -M main
git push -u origin main
```

<br/>

## Git Concepts and and Architecture

**The three trees** - git uses a 3 tree architecture
- Working Directory
- Staging Index
- Working Copy

<br/>

**Hash Values** (SHA-1) 
Git generates a checksum for each change set using SHA-1 hash algorithm, which is a 40 character hexadecimal string.
SHA-1 = code changes + meta data (parent commit, author and message) 

<br/>

**The HEAD pointer**
Pointer to the tip of current branch in repository

<br/>

## Make changes to a file
**Add files** | -
--|--
`git status` | list of untracked files and current state of changes to tracked files
`git add <filename>`	| move file to staging tree for git tracking
`git add .`	| move all files in current directory to staging
`git add tours*`	| wildcard to include all files/directories
`git add -p` | Interactively choose hunks of patch between the index and the work tree and add them to the index

<br/>

**View changes** | -
--|--
`git diff` | staging (a) vs working directory(b)
`git diff --staged` | repo vs staging
`git diff --cached`	| alias for repo vs staged
`git diff --color-words`	| more granular diff that shows word changes instead of whole lines

<br/>

**Delete files** | -
--|--
`git rm <filename>`	| similar to add but to remove a file from git repo

<br/>

 **Move and Rename files** | -
--|--
`git mv <old_filename> <new_filename>`	| Move/Rename a file

<br/>

**View a commit** | -
--|--
`git show <commit>` | see the changes in the commit  			
`git show <commit> --color-words`	| diff with color words

<br/>

**Compare two commits**  | -
--|--
`git diff <commit1>..<commit2>` | compare two commits
`git diff <commit1>..<commit2> --color-words` | -

<br/>

## Undo Changes

Undo working directory changes | -
--|-- 
`git checkout -- <file_name>`	| undo/discard changes in working directory (-- for current branch)
`git checkout -- .` |shorthand for all files
`git restore .` | TODO: new command, verify this

<br/>

**Unstage files** | -
--|--
`git reset HEAD <file_name>` | unstage changes from staging index back to working tree
`git restore --staged .`		| TODO: ?

<br/>

**Amend commits** | -
--|--
`git commit --amend -m <commit_message>` | amend previous commit. First use git add to stage changes 
`git commit --amend --no-edit` | amend previous commit and use the previous commit message

<br/>

**Retrieve old versions** | -
--|--
`git checkout <commit> -- <file_name>`	| checkout version of a file from an older commit into staging index

<br/>

**Revert a commit** | -
--|-- 
`git revert <commit>`	|revert/undo changes from an older commit

<br/>

**Remove untracked files** | -
--|--
`git clean -name`	| dry run
`git clean -feature`	| remove/discard untracked files
`git clean -n` | dry run
`git clean -dn`	| include files inside directories
`git clean -df`	| force

<br/>

## Ignore Files 

**Use .gitignore** | Pattern matching (regular expressions)
--|--
`logs/*.txt`		| ignore all text files in logs directory 
`logs/*.log[0-9]`	| anything that ends in .log and a number
`*php` <br/> `!index.php` | ignore all php files except for index.php
`node_modules` <br/>	`build` | ignore all files in a directory

<br/>

**Ideas on what to ignore**
- Compiled source code
- Packages and compressed files
- Logs and databases
- Operating system generated files
- User-uploaded assets
- Check https://github.com/github/gitignore for useful templates

<br/>

**Globally ignore files** | -
--|--
`git config --global core.excludesfile <path_to_gitignore_global_file>` | User specific instead of repo specific

<br/>

**Ignore tracked files** | -
--|--
`git rm --cachched <file_name>`	| remove file from staging index

<br/>

Track empty directories | -
--|--
`.gitkeep` | add file to empty directory
  
</details>
  
<details>
  <summary>Branches, Merges and Remote</summary>
</details>
  
<details>
  <summary>Intermediate Techniques</summary>
</details>
