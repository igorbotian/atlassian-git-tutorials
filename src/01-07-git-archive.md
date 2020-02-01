# Git Archive

## How to export a git project

Sometimes it can be useful to create an archive file of a Git repository. An archive file combines multiple files into a single file. An archive file can then be extracted to reproduce the individual files. Git is incredibly powerful at preserving history and team collaboration; however, archive files remove the overhead of Git's metadata and can be simpler to distribute to other users or preserve in long term cold storage.

### What does git archive do?
The git archive command is a Git command line utility that will create an archive file from specified Git Refs like, commits, branches, or trees. git archive accepts additional arguments that will alter the archive output.

### Git export examples
A most basic ~git archive~ example follows

```
git archive --format=tar HEAD
```

This command when executed will create an archive from the current HEAD ref of the repository. By default, git archive will stream the archive output to the ephemeral stdout stream. You will need to capture this output stream to a permanent file. You can specify a permanent file by using git archives output option or using the operating systems stdout redirection.

```
git archive --output=./example_repo_archive.tar --format=tar HEAD
```

The proceeding example will create a new archive and store it in the exmaple_repo_archive.tar file. The previous examples have both created uncompressed archive output. This is denoted by the --format=tar option. The format option also accepts popular compressed file formats zip and tar.gz. Passing one of these format options will produce a compressed archive. If a format value is not passed it will be inferred from any --output option passed.

```
git archive --output=./example_repo_archive.tar.gz --format=tar HEAD ./build
```

A partial archives of the repository can be created by passing a path argument. This example adds a ./build path argument to the archive command. This command will output an archive containing only files stored under the ./build directory

### Options

The previous examples demonstrated some of the most frequently used git-archive use cases. The following are extended options that can be passed to git-archive.

```
--prefix=<prefix>/
```

The prefix options prepends a path to each file in an archive. This can be helpful to ensure the archive contents get extracted in a unique namespace.

```
--remote=<repo>
```

The remote option expects a remote repository URL. When invoked with the remote option, git-archive will fetch the remote repository and create an archive from the specified ref if it’s available on the remote.

### Configuration
There are a few global Git configuration values that ~git archive~ will respect. These values can be set using the [git config][link to git config] utility.

```
tar.umask
```

The unmask configuration option is used to specify unix level permission bit restriction on the output archive file.

```
tar.<format>.command
```

This configuration option allows specification of a custom shell command that the git-archive output will be run through. This is similar to omitting the --output option and piping the stdout stream from ~git archive~ to a custom tool. This enables fixed custom archive post-processing.

tar.<format>.remote
If enabled this allows remote clients to fetch archives of type format.

### Git Archive Summary

Git archive is a helpful utility for creating distributable packages of git repositories. Git archive can target specific refs of a repository and only package the contents of that ref. Git archive has several output formats that can utilize added compression.
