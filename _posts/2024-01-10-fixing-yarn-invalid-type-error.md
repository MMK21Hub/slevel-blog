---
title: "Fixing ERR_INVALID_ARG_TYPE when debugging with Yarn v3 and VSCode"
layout: post
tags: javascript yarn vscode
date: 2024-01-10 10:14:00 +0000
---

When using modern versions of [Yarn](https://yarnpkg.com/) with the "Plug 'n' Play" method of storing packages, you have to use the `yarn node` command to run your program so that the Node.js runtime can access package in Yarn's format.

## My problem

This worked fine when I ran `yarn node` in the terminal, so I went on to adjust my VSCode `launch.json` to use the `yarn node` command too:

```json
{
    "name": "Launch Program",
    "type": "node",
    "request": "launch",
    "program": "${workspaceFolder}/dist/main.js",
    "runtimeExecutable": "yarn",
    "runtimeArgs": [
        "node",
    ],
    "skipFiles": [
        "<node_internals>/**"
    ]
}
```

However, when I ran that launch configuration, I got the following exception from `yarn.js`:

```none
Exception has occurred: TypeError [ERR_INVALID_ARG_TYPE]: The "path" argument must be of type string or an instance of Buffer or URL. Received null
```

This prevented me from running my program in VSCode's debugger.

## The solution

To fix this error, I had to update the version of Yarn I was using from 3.5.0 (released March 2023) to 4.0.2 (released November 2023). I did this by following the ["updating Yarn" instructions from its documentation](https://yarnpkg.com/getting-started/install#updating-yarn), which simply requires you to run two commands:

```bash
yarn set version stable
yarn install
```

In summary, if `yarn node` is giving you an inexplicable error, there's every chance that simply updating Yarn to the latest version will solve your issue.
