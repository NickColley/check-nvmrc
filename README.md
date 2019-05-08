# check-nvmrc

Repository showing how to use a standalone Node.js script to let people know they're on the wrong Node.js version.

This is useful if you have external contributors, because they may get a difficult to understand error message if they try to install your project on an old version of Node.js.

Note: This project promotes [nvm](https://github.com/nvm-sh/nvm) but you don't need to use nvm to use this approach, it just helps.

## Output

This is what users will see when they pull your project locally and try to run `npm install` or `npm start`

### If they're on a lower version (v4.0.0 vs v10.15.1)

```
You are using Node.js version 4.0.0 which we do not support. 

Please install Node.js version 10.15.1 and try again.

To do this you can install nvm (https://github.com/nvm-sh/nvm) then run `nvm install`.
```

### If they're close to the same version (v10.0.0 vs v10.15.1))

```
Warning: You are using Node.js version 10.0.0 which we do not use. 

You may encounter issues, consider installing Node.js version 10.15.1.

To do this you can install nvm (https://github.com/nvm-sh/nvm) then run `nvm install`.
```

## How to install

This repository has all the files necessary for this to work, here are the individual steps if you want them:

1. Copy [bin/check-nvmrc.js](./bin/check-nvmrc.js) into your project.
2. Copy [.nvmrc](./.nvmrc) into your project, and change the version to what you are using.
3. Add `preinstall` and `prestart` scripts to your [package.json](./package.json)

```json
{
  "scripts": {
    "preinstall": "node bin/check-nvmrc.js",
    "prestart": "node bin/check-nvmrc.js"
  }
}
```


4. (Optional) add an engines entry to package.json:

```json
{
  "engines": {
    "node": "10.15.1"
  },
}
```

## How's it work
The repostiory has a file called [.nvmrc](./.nvmrc) which the agreed version of Node.js to use for the team.

It is references a tool called `nvm` (Node Version Manager) that you can use to install different versions of Node.js

A standalone script will check the current version of Node.js being used against `.nvmrc` and warn people if they're not using the right version. This script is written with ye ol' JavaScript that works in really old Node.js versions.

## Why isn't this an npm dependency?

Older versions of Node.js can't npm install a newer projects files. So the script is written to work in older versions of Node.js without having any dependencies installed.

## I don't like something

It's just some crap scripts feel free to change it, if you think there's a mistake or something that'd be useful feel free to do a pull request though.