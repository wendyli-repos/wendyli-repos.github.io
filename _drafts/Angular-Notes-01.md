---
title: "Angular Notes 01 - Setup Angular"
date: 2020-11-01
categories: Angular Node
image: /assets/images/angular-logo.png
---
<!--excerpt.start-->
A post to record my learning notes of Angular. <!--excerpt.end--> 


# 1. Install node  
I used `nvm` to install node. My current node version is:  
```sh
$ which node 
/Users/w/.nvm/versions/node/v12.16.3/bin/node
```  
My current npm version is:  
```sh
$ which npm
/Users/w/.nvm/versions/node/v12.16.3/bin/npm
```  
My current nvm version is:  
```sh
$ nvm --version
0.35.3
```  

# 2. Install Angular CLI  
In the root directory of my computer, run below command:  
```sh
$ npm install -g @angular/cl
```  
Check if Angular is installed; & Angular version:  
```sh
$ ng --version
     _                      _                 ____ _     ___
    / \   _ __   __ _ _   _| | __ _ _ __     / ___| |   |_ _|
   / △ \ | '_ \ / _` | | | | |/ _` | '__|   | |   | |    | |
  / ___ \| | | | (_| | |_| | | (_| | |      | |___| |___ | |
 /_/   \_\_| |_|\__, |\__,_|_|\__,_|_|       \____|_____|___|
                |___/
    

Angular CLI: 11.0.3
Node: 12.16.3
OS: darwin x64

Angular: 
... 
Ivy Workspace: 

Package                      Version
------------------------------------------------------
@angular-devkit/architect    0.1100.3 (cli-only)
@angular-devkit/core         11.0.3 (cli-only)
@angular-devkit/schematics   11.0.3 (cli-only)
@schematics/angular          11.0.3 (cli-only)
@schematics/update           0.1100.3 (cli-only)
```
 
# 3. Start a new Angular project 
`cd` to project folder, then run below command:  
```sh
$ ng new my-app
```  
Then follow prompts to initiate `my-app`.

# 4. Run Angular server  
Inside the project foler, run below command: 
```sh
$ ng serve
```  


***
Reference:   
1. [Angular Set Up](https://angular.io/guide/setup-local){:target="\_blank"}  


