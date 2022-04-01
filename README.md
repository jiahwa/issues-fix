# Issues-fixed
Kinds of issues, and fixed answers

Issue.1
--
## nvm is not compatible with the "PREFIX" environment variable: currently set to "/usr/local" Run `unset PREFIX` to unset it.

logs print:
```logs
nvm is not compatible with the "PREFIX" environment variable: currently set to "/usr/local"
Run `unset PREFIX` to unset it.
.git/hooks/pre-commit: line 45: node: command not found

pre-commit hook failed (add --no-verify to bypass)
git exited with error code 1
error Command failed with exit code 1.
info Visit https://yarnpkg.com/en/docs/cli/run for documentation about this command.
```

> Fixed below

Solved it by running:`nvm unalias default`. This helped me : https://github.com/nvm-sh/nvm/issues/1645#issuecomment-856016377

logs print:
```logs
Deleted alias default - restore it with `nvm alias "default" "v14.19.0"` (Perhaps shows other default value here)
```

Also, the above operation has side effects, which can be eliminated by using the command:

```sh
nvm list
nvm use <any node version suits you>

# OR

nvm alias default stable # (Perhaps other default value)
```
