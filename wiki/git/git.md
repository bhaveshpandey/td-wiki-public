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
