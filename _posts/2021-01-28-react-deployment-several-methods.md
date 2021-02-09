---
title: "React Deployment - Several Methods"
date: 2021-01-28
tags: react deployment vercel  netlify heroku
---

<!--excerpt.start-->

A post to record procedures to deploy a React app on different CDNs. I also include some errors that encountered. <!--excerpt.end-->
> This post is a working progress, last update 09/02/2021.

## Deployment with Vercel
First time deployment :  
Step 1: Create a Vercel account;

Step 2: Navigate to project folder, and run;
```sh
> npm install -g vercel
```

Step 3: After installation completes, run
`sh vercel login `
Follow prompts to enter the email linked to the Vercel account;

Step 4: Keep all default settings;
```sh
Set up and deploy “~/Documents/Projects/words-app”? [Y/n] y
? Which scope do you want to deploy to? wendyli-repos
? Link to existing project? [y/N] n
? What’s your project’s name? words-app
? In which directory is your code located? ./

Auto-detected Project Settings (Create React App):

- Build Command: `npm run build` or `react-scripts build`
- Output Directory: build
- Development Command: react-scripts start
  ? Want to override the settings? [y/N] n

🔗 Linked to wendyli-repos/words-app (created .vercel and added it to .gitignore)
🔍 Inspect: https://vercel.com/wendyli-repos/words-app/jvkbfzkgw [1s]
⠙ Building
✅ Production: https://words-app-two.vercel.app [copied to cl
```

Step 5: Click above link and visit the site.

If anything changes later, we will need to re-deploy. Procedure is as per below.  
Step 1: Make changes of the project source codes as needed;  

Step 2: When done, inside project foler, run
`sh vercel --prod `;  

Step 3: Vercel will redeploy & update the same link.

## Deployment with Netlify  
Netlify uses a Github repo as the source of deployment so we need to create a Github repo and push all my local files into that repo. After both my local repo and Github repo are sync, then I can login Netlify to start the deployment.  
Step 1: Login Netlify and choose `New site from Git`;  

Step 2: Choose the Github repo where the React app is stored; 

Step 3: Keep all settings as default then clicl "Continue";  

Step 4: Netlify will then deploy the site.  
If your code has no warnnings, the above should make your app delpoyed. 

As my React app is a working progress, there is a `warnning` that `a 'setFlashCards' function is defined but never used`. This `warnning` does not break my app but Netlify considers it as a hard `error` and halts the deloyment. To skip Netlify from doing so, I found this [post](https://community.netlify.com/t/new-ci-true-build-configuration-treating-warnings-as-errors-because-process-env-ci-true/14434).  
According to the post, I need to set `Build command:` to `CI= npm run build` on Netlify. Hers is how to change this setting.  
Step 1: Click `Delpoys` tab;  
Step 2: Click `Deploy settings` button;  
Step 3: At the next screen `Continous Delpoyment`, under `Build settings`, change `Build command:` to `CI= npm run build`.
After the above three steps complete, redeploy, the site should be delpoyed successfully.