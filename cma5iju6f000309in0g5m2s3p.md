---
title: "Exploring Git and GitHub - Part I"
datePublished: Thu May 01 2025 15:22:03 GMT+0000 (Coordinated Universal Time)
cuid: cma5iju6f000309in0g5m2s3p
slug: exploring-git-and-github-part-i
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1743317189759/43973a8e-c4d5-46ff-b70e-b6b664263cef.png
tags: github, opensource, git, devops, cloud-native

---

**Hi everyone👋**,

This week, we're diving into the fantastic world of Git and GitHub - two must know concepts for anyone dreaming of a software development career! In this blog series on GitHub, I'll walk you through everything from installation to key topics like branching, merging, resolving conflicts, and rebasing from scratch. Plus, I'll guide you in making your first pull request! Get ready for an exciting journey with interactive visuals and animations that reveal how these version control systems work their magic behind the scenes.

This blog does not require any prior knowledge or experience with Git! Whether you're a beginner, an open-source enthusiast, or just entering the DevOps arena, Git is an essential skill to have. This is Part I of the blog series where we cover the fundamentals of git and GitHub.

So, let's jump in and get started!

---

### The What and Why behind a Version Control System?

Okay, let’s imagine a real-world scenario. You’ve started working on a **calculator project** using **Python** on your local machine. Now, you want to **team up with your friend** to develop it further.

How do you share the project? Let’s say you **upload it to Google Drive**, and your friend downloads it. Everything seems fine until the problems start.

You update some backend API. Your friend tweaks the frontend. Later, they send you a zip file with their changes. You replace your files, and suddenly **the app breaks.** Some of your changes are gone, and you have no idea what went wrong.

Now, you need to **undo everything,** but you can’t.

Now, you **wish for a time machine** to return to when everything was fine.

Well, **Git is that time machine for you!** It keeps track of all your changes, so you can easily **roll back**, **collaborate** **without overwriting** each other’s work, and never lose progress again.

That’s what a version control system does. In simple terms, it **keeps versioning your project** with every sort of change you make and stores it as a history, and you can rollback or stay at your latest version whenever needed and collaborate with your teammates with no pain point.

---

### Installing Git

Setting up git is an easy and quick process. Just navigate to this website  
[https://git-scm.com/downloads](https://git-scm.com/downloads) and download git according to your OS. Once you have downloaded, set up the environment variable and you’re done!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1745927791605/fcf2288c-84f7-4750-84e4-a34c5ff966ad.png align="center")

---

### Why Git?

You might wonder - Why Git when there are other version control systems like **Bitbucket, Mercurial or even centralised systems like SVN**?

Well, Git has become the undisputed industry standard for version control. Git stands out because it’s **fast, flexible and super popular due to its open-source nature, with a vast ecosystem and massive community support, making it the go-to choice**. It lets you work offline, try out changes safely, and easily team up with others. Plus, most platforms(like **GitHub and GitLab**) are built around Git anyway, so learning Git means you’re good to go pretty much anywhere.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1745930926466/bc4d47c7-322a-4db2-af3a-d865e284c429.png align="center")

There are mainly two types of VCS - Version Control System:  
1\. **Distributed VCS** - Everyone has the **full copy of the repo**(history and all). You can work offline, commit locally, and sync when ready.

2\. **Centralised VCS** - There’s **one central server**, and everyone **pulls/pushes changes directly** to it. You need to be online to commit.

---

### Let’s start working!

Okie, now let’s see how to work with git step by step. Consider you are working on a calculator project with a minimalistic frontend and a backend. You create a folder and navigate to it, and you have started working.

```bash
mkdir calculator-project
cd calculator-project
code .
```

Let’s say you add a basic additional functionality of adding two numbers using Python.

```python
# Get input from the user
num1 = float(input("Enter first number: "))
num2 = float(input("Enter second number: "))

# Add the numbers
sum = num1 + num2

# Display the result
print("The sum is:", sum)
```

Now you have your friend joining you for further developing and collaborating with the project and so you have to share this folder and both can work independently without overwriting the changes.That’s where git comes in!  
To integrate git with your project, navigate to the project folder and type

```bash
git init
```

**git init** means that you’re saying git “Hey git, I have started working on this project, and you just keep track of any changes to restore its history, ok?” Now any changes you make in every file are recorded, it **captures like a camera**, and you can rollback whenever needed! Isn’t it cool, tho? To verify this, type

```bash
ls -a
```

This lists down all the hidden files that start with a dot(.)Why hidden? For security purposes, like you see an **<mark>.env</mark>** file in the backend for storing passwords and usernames. You will see a new **<mark>.git/ </mark> folder** inside the project folder. Navigate to it and let’ see what’s inside it!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746073371531/c4690c4a-f6dc-4c52-bc61-bbc6778a81b1.png align="center")

Okie, that’s so huge, let me break it for you!

| config | Stores repository(folder) specific configuration like username, remote URLs, and bash shell. |
| --- | --- |
| description | Used in bare repositories; mostly ignored in normal ones |
| HEAD | A pointer where the current branch lies. In this case, it is the master. |
| hooks/ | Contains sample scripts to trigger actions at certain git events(eg, pre-commit) |
| info/ | Stores additional info like exclude file patterns(like .gitignore) |
| objects/ | contains all the content(commits,trees,blobs) in Git’s internal storage |
| refs/ | Holds references to all branches and tags in the repository. |

To view the status of your project folder,type

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746074620804/49aca7db-a3e3-4850-b841-b5922a278ff8.png align="center")

**Git status** - allows you to view the **current status of the folder**. Okay, you have added an **add.py** file and but it is **not tracked** yet. You need to **authorise it** to add it to a ready **queue**. To add it, simply type

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746075294487/f8cd3805-28a5-44a5-b017-d69063f5173f.png align="center")

As you can see, now the **add.py** file is moved to the **tracked stage(staged).**

**NOTE:** Ignore the warning message for now, as it does not affect anything!  
Now comes the important part: you need to commit your changes

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746075680937/7ef8f007-f55b-4d54-addb-c72fac14d8d6.png align="center")

**git commit** - “Alright Git, **save this change with a message** given using the -m option inside quotations!”. As you can see, one file, i.e **add.py**, is changed with 9 lines of code(inserted) and no deletion is there. When you commit, you should send a message, and it is not an optional thing.

Okay, being bored as a single? You can at least commit with git tho😅😜

Jokes apart! Once you have committed the changes, what’s next? You have to push the changes. Cool, but the real question is, push where? Let’s explore that next!

---

### Github-Quick Intro

Github is like **home for your git tracked projects** - it’s where you **store, share, and collaborate** on code with others. It provides you nice **user web interface** and allows you to contribute to opensource projects easily. It gives your Git projects a central place to live and lets the world see or contribute to them.

**Key Features**  
**Repositories** - Your project folders with code and other stuff in simple terms.

1. **Commits & Branches** - Just like Git, but you can track them visually on GitHub. It shows your commit history, commits, branches, and changes.
    
2. **Pull requests (PRs)** - Want to suggest changes? PRs let you propose edits, and others can review and merge them.
    
3. **Issues** - Like a to-do list or bug tracker for repositories (repos in short).
    
4. **GitHub Actions (CI/CD)** - Automate testing, builds, and deployments straight from your repo.
    
5. **Stars & Watching** - You can star repos like you bookmark them and watch repos to stay updated.
    

**Projects & Discussions** - For organizing tasks like kanban-style and chatting about your ideas or roadmaps.

Okay, there are so many platforms(Gitlab, Bitbucket)out there, but we use GitHub for most activities as it is easy and beginner friendly. To get started with GitHub, follow steps below

**Step 1**: Head over to **github.com** and sign up - it’s free. All you need is an email & a cool username😄.  
**Step 2**: Once you’re done, create a repo

1. Click the + icon on the top right → New repository
    
2. Name it. I love to name it as git-github-demo simply
    
3. You can leave it public/private based on preference.
    
4. Skip Readme for now (we already have our project now)
    
5. No license required for now as well (we'll look more into that later)
    

**Step 3**: Now, copy the Remote URL which we need, present under the code tab. For now, hang on with the HTTP URL itself

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746079946743/f3a390fb-cb3d-43b3-851d-9a22c25ce2d8.png align="center")

**Step 4:** Now navigate to VS Code and inside the project folder, type  
**git remote add** - with the name of the URL. I want to **name it as origin**, as it is the **default** conventional name for any remote repository, followed by the URL that you have copied before. To verify whether the folder is attached to a remote URL, cross check it by **git remote -v** and it should show the URL **with** two options both to **push and fetch** as seen below\*\*.\*\*

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746080714388/b653e1a0-cc87-489c-95b1-b902d4348065.png align="center")

Before pushing the changes, we’ll look into the branching strategy in git for sometime.

---

### Branching

Git stands out compared to other version control systems because of its **best branching strategy**. A **branch is like a copy of your codebase** where you can make changes safely, without disturbing the original code branch.

These are some branching strategies you should know

* **main/master** - This is the production-ready code, meaning people are using it in real-time applications.
    
* **dev** - A place where all active development happens before moving to the main branch.
    

**feature branch** - Created for each new feature or enhancement, mostly used for creating new pull requests.

---

How to check which branch you are working on currently? To know, simply do

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746099386472/3bab11a7-2b1f-42fa-9034-e1d871512d5a.png align="center")

**git branch** - allows you to view the branch that you’re currently working on.In this case,it’s a master branch and the star pointer that you’re seeing is the HEAD which is currently pointing to master branch.

1. **Create a new branch in the git repo, use**
    

**git branch** - **creating a new feature branch,** followed by the branch name. Let’s add a subtraction functionality to the calculator app. This **only creates a new branch without switching to the new branch,** and you’re still on your master branch only as you can see below.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746099758117/e2beae91-b983-4fe8-ba16-86b5d86cb3f9.png align="center")

2\. **Create and switch to it**

**git checkout** - It creates a **new branch and switches** to the newly created branch. Here, (-b) means branch, and checkout means switch to it. I’m adding **Division functionality**, as you can see. If you try to list out git branches, it lists **2 feature branches** and the **default master branch** with **HEAD pointing to division** branch. Cool!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746100117893/68a0b561-54da-40d4-9da9-6d6bfd58049b.png align="center")

For simply switching btw branches, just use

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746100560280/3f5bed5f-81f8-42c3-a512-ea921caa9347.png align="center")

To **delete a branch** after you’re done with a feature and it’s merged, type  
**git branch with the -d option,** followed by a branch name that you want to delete. Successfully deleted the division branch as I don’t want it anymore!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746100859464/4789059b-87f6-489f-aaa2-ac31de1729c0.png align="center")

Remember, if it’s not merged and you still want to delete,you can forcefully delete using with uppercase D.

```bash
git branch -D my-feature
```

  
Here's a complete video to help you visualize how the branching system works in Git. Shoutout to [learngitbranching.js.org](https://learngitbranching.js.org/) for making this so much easier!

%[https://youtu.be/LKgNyQ49keo] 

That’s all about Git branch, I hope that makes sense to you right now😚

---

**Forking and Cloning**

Think of forking like this: “**Hey GitHub, I love this project! Can I take a copy of it into my own account so I can play around, make changes, or contribute?**”  
When you fork a repo:  
\- You’re **creating your own version of someone else’s project** on your Github account.  
\- You can make changes without affecting the original project.  
\- It’s often the first step before **contributing to open-source**.  
But how to fork? It’s so simple. Just hang on! You will find a fork button on the top right of every git repository as given below.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746104491583/264a1738-d61e-4ca3-b2fa-2a2f7b207464.png align="center")

**Clone**  
After forking, you need the code on your local machine to work with it.That’s where cloning comes in:  
**“Hey Git, pull this entire repo from my Github account to my machine so I can code locally!”**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746104638900/0ef237f0-fff1-40dc-80a1-5bcf0db73467.png align="center")

You can do this via two ways: HTTP & SSH(Secure shell).For now, just hang on with HTTP.  
To clone, just use git clone followed by the URL that you’ve copied.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746105086994/93357054-e2de-45e2-afc2-ffa16bd75984.png align="center")

That’s about forking and cloning in github.Great job so far!

---

### Pushing changes to Github

Now let’s see how to push changes to your github repo. In the project folder, so far we have been making all additions,deletions in the master branch. But github always has main branch as their default one.So before pushing,

```bash
git checkout -b main
```

And then fetch any remote changes to your local folder.This can be done using  
**git fetch origin** \- It’s like “Hey git, go check what’s new on github, but don’t touch my local files yet. Just show me what’s changed!”.  
It just fetches the latest updates from the remote URL(origin)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746109341759/ecaa1be6-7266-4d4e-bf1e-e08d2494872a.png align="center")

Then do,  
**git pull origin main —allow-unrelated-histories** \- This command pulls changes from the main branch on GitHub and merges them into your current local branch even if their histories don’t match.Let’s look into this later!  
  
At last we can push changes to github,  
**git push origin main** - “Hey git,take all my local changes on the main branch and upload them to Github under the same branch!”

It’s like saying, “I’m done coding now save it to the cloud so others or future me can see it.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746109572128/92a0d440-8ddf-422a-8794-d1c30dcef227.png align="center")

This command shows that you’ve successfully uploaded your local commits on the main branch to the main branch on github!  
  
You can see this on GitHub as well. Tada 😄, all our files are pushed successfully!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746110511532/2f8a2396-a95d-497a-9307-fc90f2024da9.png align="center")

### Pull requests and your first contribution!

Make your very first opensource contribution here👇. I have created a sample repository for the calculator application. Please follow these steps to make some code contribution.  
1\. **Fork the repo** : Head into [https://github.com/Devisrisamidurai/git-github-demo](https://github.com/Devisrisamidurai/git-github-demo) and click on fork button and copy the main branch only.  
2\. **Clone the repo** that was recently forked on your github account using git clone via HTTP.  
3\. **Make some changes** in the code  
For now the app only has addition functionality.You can add subtraction,division etc,, or just and readme file on how to use the application giving generalized overview.  
4\. **Add the changes and commit** using git commit  
5\. **Fetch and push** the changes.  
  
Once you push, it shows raise a Pull request as given below! I have sub.py file for subtarction functionality in the subtract branch.Ensure you’re on the feature branch to make PR’s as you cannot make it in Main default branch.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746112289264/5e4133ed-b904-4d70-8115-b62dac54cc78.png align="center")

Click that , it will take you the PR description page.Give a detailed description with a clear concise title.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746112502299/f838d319-cde4-4e1d-b88c-06b6fbb75078.png align="center")

Once you’re done with this,Click on create Pull request and yeah it’s done!Congrats to you🤗

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746112581433/91a6105a-b99c-4bbb-85a7-4bc2c6143806.png align="center")

That’s it for this lecture. If you have come this far, I appreciate it💙 and wish you success on making your First Pull request! It’s a huge step in your learning process🙌

---

### Conclusion

No matter how many tutorials you watch or blogs you read (even the really detailed ones!), nothing beats **getting your hands dirty** and actually doing it. That’s where the real learning happens. So, go ahead and make your **first contribution**! Grab the repo, make sure your pull request is **meaningful** — no spammy stuff, because **only valuable PRs will get reviewed and merged**.

In this post, we’ve covered the basics: **committing changes, branching, pushing, cloning, and forking**. These are the foundation of working with Git and GitHub.

Next up in the series, we’ll dive into some more advanced stuff like **merge, rebase, and cherry-pick** — so stay tuned!  
  
Thanks for reading!  
  
Until then,Byeeee👋  

![Cute Wave Sticker - Cute Wave Bye - Discover & Share GIFs](https://i.pinimg.com/originals/cf/eb/ee/cfebee8ad262ac6f09d92dcb71e45318.gif align="left")

  
  
💡**Let’s connect!** Feel free to reach out:  
[**LinkedIn**](https://www.linkedin.com/in/devisri-s-0987b6256/)  
[**GitHub**](https://github.com/Devisrisamidurai)