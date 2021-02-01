---
title: "Deploy React On Vercel"
date: 2021-01-28
tags: vercel react deployment
---

<!--excerpt.start-->

A post to record the process to deploy a React project on Vercel. <!--excerpt.end-->

First time deployment :  
Step 1: Create a Vercel account.

Step 2: Navigate to project folder, and run
`sh

> npm install -g vercel
> `

Step 3: After installation completes, run
`sh vercel login `
Follow prompts to enter the email linked to the Vercel account.

Step 4: Keep all default settings.
`sh
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
`
Step 5: Click above link and visit the site.

If anything changes later, we will need to re-deploy. Procedure is as per below.
Step 1: Make changes of the project source codes as needed.
Step 2: When done, inside project foler, run
`sh vercel --prod `
Step 3: Vercel will redeploy & update the same link.
