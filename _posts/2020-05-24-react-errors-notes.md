---
title: "React Errors - Unexpceted end of JSON input while parsing near..."
date: 2020-05-24
categories: REACT NPM
---

<!--excerpt.start-->To record a error I encountered when running create-react-app. <!--excerpt.end-->

# Error

When I tired to run ``create-react-app`, the installing process is aborted with below error message. Error message is

```
227 error Unexpected end of JSON input while parsing near '... || ^4.0.0 || ^5.0.0 '
```

# Solution

Step 1: Run `npm clean catche -force` to clean any catche saved on my local machine inside folder `./nmp/_cacache`; this command will also create a brand new `_catche` folder.  
Step 2: Re-run `create-react-app my-app` to complete.

# Notes

- Log files are stored at `/Users/w/.npm/\_logs/`.
- The `-force` argument will force npm to fetch remote resources even if a local copy exists on disk.

---

Reference:

1. [https://github.com/facebook/create-react-app/issues/7261](https://github.com/facebook/create-react-app/issues/7261){:target="\_blank"}
