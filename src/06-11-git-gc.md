## Git gc

The `git gc` command is a repository maintenance command. The "gc" stands for garbage collection. Executing `git gc` is literally telling Git to clean up the mess it's made in the current repository. Garbage collection is a concept that originates from interpreted programming languages which do dynamic memory allocation. Garbage collection in interpreted languages is used to recover memory that has become inaccessible to the executing program.

Git repositories accumulate various types of garbage. One type of Git garbage is orphaned or inaccessible commits. Git commits can become inaccessible when performing history altering commands like [git reset](https://www.atlassian.com/git/tutorials/undoing-changes/git-reset) or [git rebase](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase). In an effort to preserve history and avoid data loss Git will not delete detached commits. A detached commit can still be checked out, cherry picked, and examined through the `git log`.

In addition to detached commit clean up, git gc will also perform compression on stored Git Objects, freeing up precious disk space. When Git identifies a group of similar objects it will compress them into a 'pack'. Packs are like zip files of Git bjects and live in the `./git/objects/pack` directory within a repository.

### What does git gc actually do?

Before execution, `git gc` first checks several [git config](https://www.atlassian.com/git/tutorials/setting-up-a-repository/git-config) values. These values will help clarify the rest of `git gc` responsibility.

#### git gc configuration

```
gc.reflogExpire
```

An optional variable that defaults to 90 days. It is used to set how long records in a branches reflog should be preserved.

```
gc.reflogExpireUnreachable
```

An optional variable that defaults to 30 days. It is used to set how long inaccessible reflog records should be preserved.

```
gc.aggressiveWindow
```

An optional variable that defaults to 250. It controls how much time is spent in the delta compression phase of object packing when git gc is executed with the `--aggressive` option.

```
gc.aggressiveDepth
```

Optional variable that defaults to 50. It controls the depth of compression `git-repack` uses during a git gc `--aggresive` execution

```
gc.pruneExpire
```

Optional variable that defaults to "2 weeks ago". It sets how long a inaccessible object will be preserved before pruning

```
gc.worktreePruneExpire
```

Optional variable that defaults to "3 months ago". It sets how long a stale working tree will be preserved before being deleted.

#### git gc execution

Behind the scenes `git gc` actually executes a bundle of other internal subcommands like [git prune](https://www.atlassian.com/git/tutorials/git-prune), `git repack`, `git pack` and `git rerere`. The high-level responsibility of these commands is to identify any Git objects that are outside the threshold levels set from the `git gc` configuration. Once identified, these objects are then compressed, or pruned accordingly.

### git gc best practices and FAQS

Garbage collection is run automatically on several frequently used commands:  
- [git pull](https://www.atlassian.com/git/tutorials/making-a-pull-request)
- [git merge](https://www.atlassian.com/git/tutorials/git-merge)
- [git rebase](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase)
- [git commit](https://www.atlassian.com/git/tutorials/saving-changes)

The frequency in which `git gc` should be manually executed corresponds to the activity level of a repository. A repository with a single contributing developer will need to execute `git gc` far less often than a frequently-updated multi-user repository.

### git gc vs git prune

`git gc` is a parent command and git prune is a child. `git gc` will internally trigger `git prune`. `git prune` is used to remove Git objects that have been deemed inaccessible by the `git gc` configuration. Learn more about [git prune](https://www.atlassian.com/git/tutorials/git-prune).

### What is git gc aggressive?

`git gc` can be invoked with the `--aggressive` command line option. The `--aggressive` option causes `git gc` to spend more time on its optimization effort. This causes `git gc` to run slower but will save more disk space after its completion. The effects of `--aggressive` are persistent and only need to be run after a large volume of changes to a repository.

### What is git gc auto?

The `git gc --auto` command variant first checks if any housekeeping is required on the repo before executing. If it finds housekeeping is not needed it exits without doing any work. Some Git commands implicitly run `git gc --auto` after execution to clean up any loose objects they have created.

Before execution `git gc --auto` will check the git configuration for threshold values on loose objects and packing compression size. These values can be set with [git config](https://www.atlassian.com/git/tutorials/setting-up-a-repository/git-config). If the repository surpasses any of the housekeeping thresholds git gc --auto will be executed.

### Getting started with git gc

You're probably already using `git gc` without noticing. As discussed in the best practices section, it is automatically invoked through frequently used commands. If you want to manually invoke it simply execute `git gc` and you should see an output indicating the work it has performed.
