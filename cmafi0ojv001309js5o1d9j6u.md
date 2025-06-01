---
title: "Exploring Git and Github Part II"
datePublished: Thu May 08 2025 15:04:51 GMT+0000 (Coordinated Universal Time)
cuid: cmafi0ojv001309js5o1d9j6u
slug: exploring-git-and-github-part-ii
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1746455147199/b32c94ce-fa5c-41e1-a0a6-8b7408007ef9.png
tags: github, opensource, git, devops

---

**Hi everyone,**

Welcome back to the second part of our Git & Github series. In [part I](https://devisri-blogs.hashnode.dev/exploring-git-and-github-part-i), we have explored the basics from setting up a git repo to branching, committing, pushing and forking, all with a simple calculator app step by step while making your [first Pull Request!](https://devisri-blogs.hashnode.dev/exploring-git-and-github-part-i#heading-pull-requests-and-your-first-contribution)

Now it’s time to level up! In this part, I’ll walk you through other concepts like **merging, rebasing, cherry-picking**, how to deal with **merge conflicts** and some important concepts in git to get well grounded. We’ll also touch on how to work with an opensource project on **raising an issue, pull requests**, look into **licensing a project**!

If you haven’t checked Part I yet, do so [here](https://devisri-blogs.hashnode.dev/exploring-git-and-github-part-i) to better understand things. So without any further ado, let’s get started!

---

### A quick Recap!

So far, we know how to initiate a project with git, make changes, add them, and eventually commit, followed by pushing the changes to the Github repository. We have also worked with remote URLs by creating a separate branch, and we made our first pull request successfully by building a simple calculator application!

Now let’s see what happens after that!

By now, we have made several commits in the project repository. How can we check the history of the commits? Let’s talk git logs.

Once you’ve committed a few changes, you might wonder: **”Wait, what did I even do last week?”** That’s where **git log** comes in - it’s like your **project’s timeline** or journal, showing every commit you’ve made. Just do,

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746533903073/adccaaba-2adf-41fc-bbbd-6f4bdd1eb098.png align="center")

As you can see above, it clearly shows  
**On what date and time**, **which person? On which branch?**  
made changes showcasing their name and email address as well. It also shows whether it’s just the commit and its status, whether merged or not, showing with the commit message when we did git commit.  
Pretty cool, right?

But sometimes it looks a bit too long and messy. So here’s a cleaner version of this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746534342977/a5ca905f-ea2b-4d7c-bfb7-43ceff79ccae.png align="center")

**git log --oneline** - This shows each commit in a short and sweet format, **just one line per commit**.Super helpful when you just want a **quick overview** of what happened.

In the above examples, we saw the logging details of the master/main branch. If you wanna see the **commit history for a specific branch**, then do git log followed by branch name.Simple nah?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746534533819/e15ce493-3a19-4713-bdbb-0b99782bab27.png align="center")

Tada😄, It shows the commit history for that specific branch(subtract) only. This would be useful specifically when you’re working on multiple features at once and need to check the context.

And sometimes, we just forget everything. We would be juggling across multiple commands like what command to use at which time, what specific options are attached to it, and that’s perfectly fine, you don’t have to worry about it cuz Git got you back! If you do  
**git help** → It shows a bunch of commands, and you really don’t wanna memorise & remember all of those necessarily. Whenever you need some help, git has a Bible(like quick revision after a long time) and can guide you through to resolve all your problems! Anytime git is for you🫂!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746535035696/fe7e11d9-937b-442f-af2b-90469073c080.png align="center")

If you want help with just a **specific command,** then use **git help &lt;command&gt;**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746535425812/cc3be63f-a5aa-488d-b6ad-bbf109008f44.png align="center")

This takes you to the **default browser** with the **cheatsheet** for that command, giving all the info about what the command does, different options, and examples like those seen below(I have cropped, it’s very detailed)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746535600261/842f7934-ae3c-4cc8-9ab1-94de731f0b7d.png align="center")

Well, that’s something you need to be aware of, the logging details! Let’s move on to the next topic.

---

### Rollback & Revert in Git(The undo option)

So let’s say you have made some potential changes to the calculator app in the addition functionality by adding the feature of adding three numbers at a time. But as time grows, you see that people are not using that special feature or let’s say it breaks the running application, which should not happen, so to speak!  
You are in the thought of “ Hmm… I don’t think I needed that change….”

Now you want to undo that commit and just go back to the previous version of the running application.Git has your back with some undo options.  
So to do that, simply

**git reset** - It’s an **undo button↩️ for your git repo**. It let’s you to roll back to a previous state in your commit history. This tells git, **"Hey git, take me back to this specific commit and erase everything after that like it never happened!”**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746545730285/0f7d1181-0f63-4f05-9ae9-617d89c8a153.png align="center")

You can simply copy the **commit ID** (the string you’re seeing before the commit message)  
But what is that option -- hard means?  
**The -- hard flag will also remove any uncommitted changes** in your working directory\*\*.\*\* So use this if you’re only 100% sure.

But what if you want to keep your changes? then use  
**\--soft** - Let’s say you want to **undo the commit but keep your code in place** may be you want to edit and recommit.

**\-- mixed** - Use this if you want to **unstage the changes**(**but not delete them**).Super helpful when you mess up a commit message or need to clean your commit history.

```bash
git reset --soft HEAD~1
```

This just undoes the last commit, keeps all your code, and gives you a chance to fix things. It’s like saying,**“wait, git, I need a do-over… but don’t throw my code away”**.

For now, I’m sure this **seems very confusing🫠** for you cuz I have been there as well. Let’s deep dive into this and do some real work together! Have some patience!

Now, in the current calculator application with just addition and subtraction functionality, I’m now adding multiplication as well, but I’m introducing some bugs. I have placed the **division(/) instead of the (\*) symbol** in the code.

```python
# Function to subtract two numbers
def multiply(x, y):
    return x / y

# Test the subtraction functionality
if __name__ == "__main__":
    print("Welcome to the Calculator Program!")
    
    num1 = float(input("Enter the first number: "))
    num2 = float(input("Enter the second number: "))
    
    result = multiply(num1, num2)
    
    print(f"The result of {num1} * {num2} is {result}")
```

**CASE 1**: Before knowing it was a bug, I made a git commit, and then realized it was a mistake later. So to undo the commit, simply do

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746547194314/cb838e7f-4e4d-45ae-9136-aed058b5c239.png align="center")

This command just undo the commit. But the code is still there in staged mode (which means it’s added). Cool!

**CASE 2**: Now fix the bug and recommit it using git commit. Now let’s say you want to unstage the file too(You’re not ready to commit anything):

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746547559017/8e3251aa-2b2f-4fcf-8530-66282395a0cc.png align="center")

You need to do git add again :( to commit the changes.

**CASE 3**: Let’s say you want to wipe out that bad commit and also delete the buggy code entirely:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746547833790/63e9139c-06b1-4e0e-8f37-d762bf1f8bac.png align="center")

Now, if you do check the status and logs,

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746547889466/4fa50ba5-2389-4162-a803-34f1f5e0e2d2.png align="center")

you can see there are no changes made, and the commit is erased fully! Be careful when you do this.

And that’s a wrap about the major diff btw soft, hard and mixed options.

---

### **Merge & Rebase & Cherrypick**

Okie, consider this:  
You and your friend are working on two different features of the same calculator app.  
You’re working on multiply branch.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746695256778/0c635140-0f9f-44fe-9ed7-c0690d670c2e.png align="center")

Then, your friend adds Division to the main branch.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746695565721/0747611a-de20-4595-8aed-d78c2ada6166.png align="center")

Now you both want your work to live happily together, but git needs to merge your changes without stepping on each other’s toes.

Let’s see how merging and rebasing help you do just that.

The end goal is same here, you want to merge the changes from one branch to another but both do in its own unique way.

**CASE 1**: **git merge**

Merging keeps track of that merge with a new commit.It makes a new commit when you merge something.

Imagine you’re on main and you’ve finished the multiply branch and want to pull it to main.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746698560302/428d6d4f-2f0b-4d7d-af6e-628a5f46e2e0.png align="center")

Git combines changes from feature with main and creates a merge commit as given below. Ensure you’re on the main branch whenever you’re merging.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746705071807/25b9b4c0-1b43-47ed-81b4-80668d1be2a5.png align="center")

**git merge** → allows you to merge one feature branch to the main branch.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746705234041/8daf43fe-a031-4acc-bfc2-adec6a553834.png align="center")

**git log --oneline --graph --all** → allows you visualize the commit graph showing where branches diverged and merged.

**Why merge?**

* Keeps history clearer - you can see exactly when and where branches joined.
    
* Great for teams working on separate features.
    
* Works perfectly when creating PRs on GitHub (GitHub actually uses merge by default!).
    

**CASE 2: git rebase**

Now let’s say your multiply branch has multiple or atleast a few commits, but main has also moved ahead(addition features may be updated for three nums)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746698299476/fd156a08-dec4-403d-ad79-6b74ba000f6b.png align="center")

If you try to merge now, your commit history might get messy.

Instead of merging commits, you can use rebase to “replay your commits” on top of the latest main.

It's like, **“Hey git, please take all my work and pretend I did it after what’s on my main. Gotcha?**”

Now your multiply branch is super clean,as if it was created after the latest main.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746705867254/583df406-4217-4698-a0e3-ce17db032ab4.png align="center")

If there are any conflicts, git will pause and show you the conflicted files. To resolve, manually edit the conflicted files to fix the issues. Then run the below command and repeat until the rebase completes.

```bash
git add <filename>
git rebase --continue
```

That’s all about merging and rebasing!

**CASE 3: Cherry pick**

There are times **when you don’t want to merge an entire branch, you just need a specific commit from it**. That’s exactly what git cherry-pick is for.

You’re working on the main branch, and there’s a useful bug fix on a feature-fix branch. The rest of the branch isn’t ready to be merged, but you need that one fix.

```bash
git checkout main
git cherry-pick <commit-hash>
```

Use cherry pick when you need only one or a few commits, not the full branch. This would be particularly useful for hotfixes or selectively reusing changes to keep your branch’s history focused and clean.

Make a lot of commits and get your hands dirty by playing around with these commands to build a strong foundation. Alright, Cool!

---

### Resolving merge conflicts!

A merge conflict **happens when two branches make changes to the same part of file, and git goes to a confused state** as it does not know which change to keep forever.

For example,Consider this scenario  
You change line 10 of the **addition.py** file in the **multiply branch**. Your teammate changes line 10 of the **addition.py** file in the **main branch**.

When git tries to merge the branches, it gets confused: \*\*“Which version of line 10 should I keep?”  
\*\*Git then pauses the merge and asks you to resolve the conflict manually.

**Github Issues**

They’re just simple ways to **talk about bugs,improvements,or questions** in a project.You open one when something’s not working or if you have a suggestion like raising your hand and saying,”Hey,I found this!”.

**Github discussions**

It’s a space for **open conversations around a project** like asking questions, sharing ideas ,or getting help. Discussions are more casual and community-driven. It’s great for keeping the project interactive and welcoming!

---

### Licensing a project

When you’re creating a repo on github,it asks for licensing the project. But what is that? A license is a **legal document that tells others what they are allowed(or not allowed) to do** with your code. (providing RBAC)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746716564025/75412f8c-199d-4e98-907f-ddb5c220a5fc.png align="center")

It answers questions like  
1\. Can someone use your code in a commercial product?  
2\. Do they have credit for you?  
3\. Can they modify and redistribute it?

| **License** | **Usecase** |
| --- | --- |
| ***MIT*** | Use when you want to **allow anyone to do anything** with your code, as long as they give you credit. |
| ***Apache 2.0*** | Use when you want **MIT**\-like freedom **plus protection** from patent claims. |
| ***General Public License v3 (GPL)*** | Use when you want any **modified version** of your code to also be **open-sourced** under the same license. |
| ***Mozilla Public License 2.0(MPL)*** | Use when you want to **keep modifications** to your files open-source but allow **linking with proprietary** code. |
| ***BSD 3-Clause*** | Use when you want to allow **permissive licensing like MIT**, but with **minimal attribution** and endorsement clauses. |

For your repository to truly be open source, you'll need to license it so that others are free to use, change, and distribute the software.

These are the major licenses(there are pretty few) we use for the projects in general, providing access with some rules. That’s all about licensing a GitHub project!

---

### How opensource projects work with git?

Every project whether it's small, big, or open-source uses **Git** to manage things smoothly. From popular tools like **Kubernetes**, **Docker**, to even **Vim**, Git plays a key role in handling code changes, keeping history, and helping teams collaborate without messing things up.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746715098058/87ae1d0e-cdc4-4485-a4dd-6bca21abb6f5.png align="center")

It’s honestly become an essential part of software development. Git takes care of a lot of the manual effort, like tracking changes, handling different versions, and merging work from multiple people. Plus, it works well with other tools, which makes it even more powerful.

**GitHub**, which has been maintained by **Microsoft since 2018**, takes Git to the next level by putting your project online where others can see it, contribute, or report bugs.

---

### Conclusion

That’s all for nowand we made it to the end of the blog together🙌! We’ve learned some really useful Git commands like `git log`, `rebase`, `merge`, and `reset`. We also saw why licenses matter and how open-source projects use Git and GitHub to work together smoothly.

I know it might feel like a lot at first, but don’t worry😄 - the best way to learn Git is by using it. Try things out, practice with a small project, and soon these commands will feel easy and natural for you.

If you made it till the end, I truly appreciate your time💙. If you found this helpful, feel free to like it or share it with your friends who might need it too.

**Thank you so much for reading!**

Until next time, byee 👋

![Wave Bye Sticker - Wave Bye Goodbye - Discover & Share GIFs](https://i.pinimg.com/originals/59/d1/71/59d17122934ef58fb24fda82d8854214.gif align="left")

💡**Let’s connect!** Feel free to reach out:  
[**LinkedIn**](https://www.linkedin.com/in/devisri-s-0987b6256/)  
[**GitHub**](https://github.com/Devisrisamidurai)