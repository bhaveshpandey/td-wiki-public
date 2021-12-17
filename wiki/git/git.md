# Git

Following are some tips and tricks which I have found useful over time.

## Multiple accounts using ssh keys (Github / Gitlab)

This is not really directly related to git however important and relevent enough to find a mention here. Authentication over ssh while maintaining multiple accounts over multiple services (Github, Gitlab etc) is really annoying.

There are 2 ways to go around this.
1. A config file at: ~/.ssh/config
2. Adding the public keys to the ssh-agent using
    ```shell

    ssh-add /path/to/key
    ```

I lean more towards **2** as its relatively easy and since **1** seems more of a hassle.

Have a look at this blogpost:

[Maintaining multiple git accounts using SSH](https://coderwall.com/p/7smjkq/multiple-ssh-keys-for-different-accounts-on-github-or-gitlab)

## Restore/rollback to earlier commit of a file.
```git
git restore /path/to/file
```

## Creating an empty branch

Recently, I realized that creating a new repo/project on Gitlab doesn't create a default main branch.
Unfortunately I had already setup a feature branch to work on (not realising about the non-existent main branch). This also made this feature branch the default branch (yikes!).

To remedy this, I created an empty **main** branch, pushed that to remote. Set that as the new default and merged the feature branch in as usual. I think this can be quite handy in a tricky situation.

```shell

# Create an orphan branch
git checkout --orphan main

# Remove all the contents
git rm -rf .

# Need at least one commit before we can push to github/gitlab
git commit --allow-empty -m "main branch. freshly minted :)"

# Push
git push -u origin main
```

## Extract a child directory inside a repo into a separate git repo

This is incredibly useful for the times when we need to restructure a git repository.

[Git filter-repo example](https://ptc-it.de/move-files-to-new-repo-in-git/)

```shell

git remote remove origin
git filter-repo --path "path/to/file1" --path "path/to/file2" --path "dir1"
```
