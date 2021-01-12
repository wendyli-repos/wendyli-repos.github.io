---
title: "React Errors - Unexpceted end of JSON input while parsing near..."
date: 2020-05-24
categories: REACT NPM
---

<!--excerpt.start-->To record a error I encountered when running create-react-app <!--excerpt.end-->

# Error

When I tired to run ``create-react-app`, the installing process is aborted with below error message. Log file location is /Users/w/.npm/\_logs/.  
Log detail is

> 227 error Unexpected end of JSON input while parsing near '... || ^4.0.0 || ^5.0.0 '

# Solution

Step 1: Run `npm clean catche -force` to clean any catche saved inside folder `./nmp/_cacache`; this command will also create a brand new `_catche` folder.
Step 2: Rerun `create-react-app my-app` to complete.

# Notes

> The `-force` argument will force npm to fetch remote resources even if a local copy exists on disk.

```sh
$ printenv
```

## To open environment variable

Open and edit environment variable in a `nano` editor.

```sh
# ensure pwd is the root directory
$ nano .bash_profile
```

The alternation is to open in a `vi` editor.

```sh
# ensure pwd is the root directory
$ nano .bash_profile
```

## To save changes in `.bash_profile`, press `Control` + `O`.

## TO exit `nano` editor, press `Control` + `X`.

# Python related

# Node related

# Ruby related

---

Reference:

1. [https://github.com/facebook/create-react-app/issues/7261](https://github.com/facebook/create-react-app/issues/7261){:target="\_blank"}
