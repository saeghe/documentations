## Introduction

You can use the `add` command to add a git repository to your application as a package.

As a package user, simply search online, and as soon as you reach the git repo, you can add it.

As a package developer, there is no need to register your package in other places.
Your package is ready to use as soon as you push it to the git.

## Usage

Adding a package to your application using the `add` command is very easy.
You only need to provide a path to your desired package, and it adds that package to your application.

The path can be a HTTPS path or SSH path to the package.

For a HTTPS path use:

```shell
saeghe add https://github.com/{owner}/{repo}.git
```

For SSH path use:

```shell
saeghe add git@github.com:{owner}/{repo}.git
```

You can simply add any package to your application using this single command.
Remember to replace `{owner}` and `{repo}` with your desired package owner and repo name.

Alternatively, you can define an alias for a package and use the alias for adding the package.

```shell
saeghe alias package-alias git@github.com:{owner}/{repo}.git
saeghe add package-alias
```

> **Note**
> For more information about the `alias` command,
> please read [this documentation](http://saeghe.com/documentations/alias-command).

By default, it checks the given package's repository to see if there are any releases for the package.
If it finds releases, it downloads the latest release of the package for your application,
unless you specify the version tag that you wish to install.

```shell
saeghe add https://github.com/{owner}/{repo}.git --version={tag-name}
```

In this case, it adds the same version of the package to your application.

However, sometimes you may need a development version of a package.
In this case, you can specify `development` as the version tag, and it clones the package for your application.
Cloning the package also happens when there is no release for the package.

> **Note**  
> For reading packages, Saeghe needs a token. 
> You either, should have an environment variable named `GITHUB_TOKEN` containing a GitHub Token, 
> or you need to add one using the `credential` command.
>
> For more information about the `credential` command, 
> please read [this documentation](http://saeghe.com/documentations/credential-command).

## Example

Let's say you need to install the `test-runner` package to our application.
The owner of this package is `saeghe` and the repo is `test-runner`.
You only need to run:

```shell
saeghe add https://github.com/saeghe/test-runner
```
And it will install the package to `Packages/saeghe/test-runner` on your project directory.

You will see the package in your `saeghe.config.json` file under the `packages` section:

```json
"packages": {
    "git@github.com:saeghe\/test-runner.git": "version-number"
}
```

The package metadata will be added to the `saeghe.config-lock.json` file:

```json
"git@github.com:saeghe\/test-runner.git": {
    "version": "version-number",
    "hash": "hash-for-installed-version",
    "owner": "saeghe",
    "repo": "test-runner"
}
```

