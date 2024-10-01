# Git Commands
====

Quick start
----

`git pull --rebase`

`git add .`

`git commit -m "commit message"`

`git push`


# Let's get started
----

```sh
git --version
```

`git --version` - Check git version

## Git Init 
----

```sh
git init
```

### What Does `git init` Do?

`git init` is one way to start a new project with Git, create a new local repository, initialize a new repository in your current directory. To start a repository, use either `git init` or `git clone` – not both.

To initialize a repository, Git creates a hidden directory called `.git`. That directory stores all of the objects and refs that Git uses and creates as a part of your project's history. This hidden `.git` directory is what separates a regular directory from a Git repository.

### How to Use `git init`

#### Common usages and options for `git init`

* `git init`: Transform the current directory into a Git repository
* `git init <directory>`: Transform a directory in the current path into a Git repository
* `git init --bare`: Create a new bare repository (a repository to be used as a remote repository only, that won't contain active development)

You can see all of the options with `git init` in [git-scm's documentation](https://git-scm.com/docs/git-init).

### Examples of `git init`

#### `git init` vs `git clone`

Starting a new project can be confusing. Sometimes, it's unclear if you should use `git init`, `git clone`, or both.

##### `git init`: One Person Starting a New Repository Locally

Your project may already exist locally, but it doesn't have Git yet. `git init` is probably the right choice for you. This is only run once, even if other collaborators share the project. 

- First, initialize the repository. 
- Once you have initialized the repository, create a remote repository somewhere like GitHub.com.
- Then, add the remote URL to your local git repository with `git remote add origin <URL>`. This stores the remote URL under a more human-friendly name, `origin`.
- Shape your history into at least one commit by using `git add` to stage the existing files, and `git commit` to make the snapshot.
- Once you have at least one commit, you can push to the remote and set up the tracking relationship for good with `git push -u origin main`.

##### `git clone`: The Remote Already Exists

If the repository already exists on a remote, you would choose to `git clone` and _not_ `git init`.

If you create a remote repository first with the intent of moving your project to it later, you may have a few other steps to follow. If there are no commits in the remote repository, you can follow the steps above for `git init`. If there are commits and files in the remote repository but you would still like it to contain your project files, `git clone` that repository. Then, move the project's files into that cloned repository. `git add`, `git commit`, and `git push` to create a history that makes sense for the beginning of your project. Then, your team can interact with the repository without `git init` again.

#### `git init` Existing Folder

The default behavior of `git init` is to transform the current directory into a Git repository. For an existing  project to become a Git repository, navigate into the targeted root directory. Then, run `git init`.

Or, you can create a new repository in a directory in your current path. Use `git init <directory>` and specify which directory to turn into a Git repository.

### `git init` Gone Wrong

#### `git init` in the wrong directory

Running `git init` in the wrong place will create unintended repositories. You may have noticed strange error messages when using Git. Maybe you suspect that another parent directory is also a Git repository.

To fix this, you first need to track down which directory is the unintended repository. Use `git status` to see if the current directory is tracked by Git. If it is, you can either run `ls -al` and look for an otherwise hidden `.git` directory. 

If you don't see it, navigate one level up in the directory structure with `cd ..`. Use `git status` again in combination with `ls -al`. Repeat this until you find the `.git` directory.

Once you find the `.git` directory, and you are sure that you don't want that to be a Git repository, use `rm -rf .git`. This will remove the `.git` directory, effectively un-initializing that repository. Run `git status` again to confirm that Git is no longer tracking any of these files. (It could be possible that multiple layers of `.git` directories are present.)

Return to your working repository, the one that you _expect_ to be under version control. Things should be working as expected.


`git help <command>` - Get help with a specific git command.


# Checking what's up
----

## Git Status
----

```sh
git status
```

### What Does `git status` Do?

`git status` Shows the current status of your repository, including any files that have been modified, added, or deleted since the last commit, and files currently staged for commit. 
When in doubt, run `git status`. This is _always_ a good idea. The `git status` command only outputs information, it won't modify commits or changes in your local repository.

A useful feature of `git status` is that it will provide helpful information depending on your current situation. In general, you can count on it to tell you:

- Where `HEAD` is pointing, whether that is a branch or a commit (this is where you are "checked out" to)
- If you have any changed files in your current directory that have not yet been committed
- If changed files are staged or not
- If your current local branch is linked to a remote branch, then `git status` will tell you if your local branch is behind or ahead by any commits

During merge conflicts, `git status` will also tell you exactly which files are the source of the conflict.

### How to Use `git status`

#### Common usages and options for `git status`

- `git status`: Most often used in its default form, this shows a good base of information
- `git status -s`: Give output in short format
- `git status -v`: Shows more "verbose" detail including the textual changes of any uncommitted files

You can see all of the options with `git status` in [git-scm's documentation](https://git-scm.com/docs/git-status).


`git diff` - Lists every individual change to every file that has changed since the last commit. Add the '--staged' tag to show changes currently staged for committing.

Committing
----

`git add .` - Add all current changes to the staging area, ready for the next commit.

`git add -p <filename>` - Add some changes in `<filename>` to the staging area, ready for the next commit.

`git commit -a` - Commit all local changes in tracked files to the staging area, ready for the next commit.

`git commit` - Commit previously staged changes.

`git commit <filename> -m 'My commit message'` - Commits changes to the `<filename>` file.

> * The `-m` flag expects to be followed by a commit message surrounded by quotes.
> * Single quotes if you want to use quotation marks in your message, or double quotes if you want to use apostrophes in your message.
> * If you want to commit everything in a sub directory, `git commit sub-dir -m 'message'`.
> * If you want to commit everything in the repo without staging it first (_dangerous_), `git commit -a -m 'message'`.


`git commit --amend` - Change the last commit. *Don‘t amend published commits!!*

Commit History
----

`git log --oneline` - Show all commits, starting with newest. The oneline flag cleans the entries up a bit to display each commit on one line.

`git log -p <file-name>` - Show changes over time for a specific file.

`git blame <file-name>` - Display who changed what in `<file-name>`.

`git blame -L 10,20 <file-name>` - Will display who edited those specific lines of `<file-name>`.

Branching Out
----

`git checkout <branch-name>` - Allows you to switch between git branches, adding the `-b` flag creates the branch you are switching to if it doesn't already exist. You can also specify specific commit hashes instead of branch names.

If you want to checkout a specific file you can `git checkout <branch-name-or-commit> <file-path>` which is powerful as it allows you to selectively merge in files or rewind changes.

`git branch` without any parameters will list all current branches. You can also use it to create a new branch with `git branch <new-branch-name>` which will create a branch based on your current HEAD but not check it out (which is why `git checkout -b <new-branch-name>` is so useful).

`git checkout --track <remote-name>/<branch-name>` - Create a new tracking branch based on a remote branch.

`git branch -d <branch-name>` - Delete a local branch.

`git push origin --delete <branch-name>` - Delete a remote branch.

`git tag <tag-name>` - Mark the current commit with a tag.

Phoning Home
----

As evidenced by the popularity of remote repo hosting services (hello Github!), One of the most powerful features with git is the ability to track remote repositories.

`git remote -v` - List all currently configured remotes. The `-v` flag stands for *verbose* and allows you to see more information about the remote repos, like the url.

`git remote show <remote-name>` - Show more information about a specific remote.

`git remote add <remote> <url>` - Add new remote repository, named `<remote>` and with a source url of `<url>`.

`git fetch <remote>` - Download all changes from `<remote>`, but don‘t integrate into HEAD.

`git fetch --dry-run -v` -  `--dry-run` Show what would be done, without making any changes. `-v` Be verbose.

`git pull <remote> <branch-name>` - Download changes and directly merge/integrate.

`git push <remote> <branch-name>` - Publish local changes to the remote repo.

`git branch -dr <remote-name>/<branch-name>` - Delete a branch on the remote repo.

`git push --tags` - Publish any tags you've added.


Making Synergy!
----

Dealing with differences and changes between repos is the real power behind git.

`git merge <branch-name>` - Merge `<branch-name>` into your current HEAD.

`git rebase <branch-name>` - Rebase your current HEAD onto `<branch-name>`. *Don‘t rebase published commits!!*

`git rebase --abort` - Aborts a rebase in progress.

`git rebase --continue` - A rebase will pause when it detects a conflict and will wait for you to *resolve* it/them by choosing which side of the merge to keep. When you've resolved the conflicts, this command continues the rebase.

`git mergetool` - Use your configured merge tool to solve conflicts.

`git add <resolved-file>` - Use your editor to manually solve conflicts and (after resolving) mark file as resolved.

`git rm <resolved-file>`

Ctrl/Cmd-Z!
----

We all make mistakes.

`git reset --hard HEAD` - Discard all local changes in your working directory.

`get checkout -f` - Discard all local changes in your working directory. (same behavior as `git reset --hard HEAD`)

`git checkout HEAD <file-name>` - Discard local changes in a specific file.

`git revert <commit>` - Revert a commit (by producing a new commit with contrary changes).

`git reset --hard <commit>` - Reset your HEAD pointer to a previous commit and discard all changes since then.

`git reset <commit>` - Reset your HEAD pointer to a previous commit and preserve all changes as unstaged changes.

`git reset --keep <commit>` - Reset your HEAD pointer to a previous commit and preserve uncommitted local changes.

Tips and Tricks
----

``git checkout -- `git ls-files -m` `` - Reset modified files in a directory

``rm -rf `git ls-files --other --exclude-standard` `` - Remove untracked files (use caution)

`git log -G "<search-string>" --pretty=format:"%C(yellow)%h %Creset%s %Cgreen(%cr) %Cblue[%cn - %ce]" --decorate` - Search commits for a string or code

The following snippet is handy if you're dealing with a monolithic repo with many branches and submodules:  
``git checkout <branch-name> && rm -rf `git ls-files --other --exclude-standard` && git submodule update --init --recursive`` - Reset-checkout.. checks out branch, removes untracked files, and re-inits submodules
