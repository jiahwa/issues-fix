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

Issue.1
--
## TypeError: require.context is not a function.

logs print:
```logs
const demos = require.context(path, false, regExp);
                        ^

TypeError: require.context is not a function
```

> Fixed below

Solved it by `polyfill` for require.context. Thie helped me : https://gist.github.com/ezidio/f64c59d46b19a3fe671a9ded6441de18

Code is like :

```js
const path = require("path");
const fs = require("fs");
require.context = (base = '.', scanSubDirectories = false, regularExpression = /\.js$/) => {
        const files = {}
    
        function readDirectory (directory) {
            fs.readdirSync(directory).forEach((file) => {
            const fullPath = path.resolve(directory, file)
    
            if (fs.statSync(fullPath).isDirectory()) {
              if (scanSubDirectories) readDirectory(fullPath)
              return
            }
    
            if (!regularExpression.test(fullPath)) return
              files[\`./\${file}\`] = true
            })
        }
    
        readDirectory(path.resolve(__dirname, base))
    
        function Module (file) {
            return require(path.resolve(__dirname, base, file))
        }
    
        Module.keys = () => Object.keys(files)
    
        return Module
        }
```
