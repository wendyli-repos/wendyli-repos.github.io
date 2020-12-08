---
title: "TypeScript Notes 02 - TypeScript Commands"
date: 2020-11-03
categories: TypeScript
<!-- image: /assets/images/angular-logo.png -->
---
<!--excerpt.start-->
A post to record my learning notes of TypeScript. <!--excerpt.end--> 


# 1. Commands 
`$ tsc init`  
`$ tsc -w`

2. Change root and out dir in `tsconfig.json`
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






