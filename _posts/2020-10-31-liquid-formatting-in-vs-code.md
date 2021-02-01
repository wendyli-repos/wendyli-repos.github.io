---
title: "Formatting Liquid in VS Code"
date: 2020-10-31 
categories: VSCode, Jekyll
---

I use VS Code as text editor to learn Javascript then I cannot escape from the fate to install the code formatter - Prettier. No doubt that Prettier is the opinionated formatter and made my begineer's JS coding experience very happy. You cannot deny that it is satisfying to see all codes neatly formatted.   
While I moved on to build my portfolio with Jekyll when Prettier gave me a very hard time to format everything the way it wanted. After many trial and error, I finally get a formatter setup and running. Here are some steps:
### Steps:
1. Create a workspce in VS Code;
2. Disable "Prettier" for this workspace;
3. Install "Liquid" extension;
4. Go to "settings.json" file in VS Code and choose the tag "WORKSPACE";
5. Search "liquid.format" and "liquid.rules";
6. Copy the search results from above to "WORKSPACE" setting;
7. Set "liquid.format"'s value to "true" if it is false;
8. Restart VS Code and open the workspace;
9. Any *.html should be formatted by "Liquid" nows. 

I reckon there should be other better ways to but the above solves my problem for now. If any better ideas, feel free to drop me a line on Github. Cheers. 
