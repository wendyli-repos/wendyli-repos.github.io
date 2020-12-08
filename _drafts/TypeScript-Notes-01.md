---
title: "TypeScript Notes 01 - Install TypeScript"
date: 2020-11-02
categories: TypeScript
<!-- image: /assets/images/angular-logo.png -->
---
<!--excerpt.start-->
A post to record my learning notes of TypeScript. <!--excerpt.end--> 


# 1. Install TypeScript  
In the root directory of my computer, run below command:  
```sh
$ npm install -g typescript
```  
After installation is completed, type below command to check version:  
```sh
$ tsc --version
Version 4.1.2
``` 

# 2. Create TypeScript file
All typescript file end with `*.ts`. 

# 3. Compile TypeScript file to JavaScript file  
All TypeScript files will be compiled to JavaScript files before being executed. 
```sh
$ tsc main.ts
```  

# 4. Run JavaScript file in terminal
```sh
$ node main.js
```  
Shortcut to compile and run *.js at the same time:
```sh
$ tsc main.ts | node main.js
```



