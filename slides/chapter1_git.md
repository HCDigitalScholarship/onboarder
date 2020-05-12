---
type: slides

---

# Git and version control

We use git for everything.  You may already know and use it.  Whatever you already know, we'd like to spend a few minutes talking about how we use Git and what we exect you to know.  


---

Always first:
```git pull ```

If you're in a project directory that is tracked by git, `git pull` will check with GitHub for any new changes and update your local copy.  Imagine spending an hour writing code, it's brilliant, only to get a "merge conflict."  Someone else already wrote that.  

---

You can also:
```git status```

This will show any differences between your copy of the project and the repository. If you've added new files that need to be tracked, they'll appear in red.  As a habit, it's good to `git status` before you start a commit.  This will help you establish what's new and what will be added to the commit.

---

```git checkout```
This command is used to switch branches. The default branch is `master`. For many projects, you'll be asked to work on your own branch or to create a branch for each issue. You can change branches with `git checkout branch_name`. If you want to create a branch and move into it enter `git checkout -b ajanco`.    

---

```git add```
When you create a repository you use `git init`.  This tell git to track changes in a directory and its subdirectories. As you add new files to the folders, you need to tell git to track them.  You can use `git add .` to track all files, but this is sloppy.  Many many times you'll have throw away files or files with sensitive information that you don't want to push to GitHub. Just `git add my_file.txt` and it will start tracking a new file. 

---

```git commit -am "commit message"```
Now you just need to commit your changes.  The `-a` tag will include changes to all tracked files and `-m` appends a message.  Commit messages are not for you.  They're a message to other coders that explains what was accomplished in the commit. It's very tempting to flake on this and write "changed stuff" or "fixed bug."  In the commit we can see the changes that were made.  What we don't know is why the changes were made.  Give some context, name the issue or problem that you addressed: "Fixed Issue #23: images now sized correctly on mobile."     

---

```git push```

Now that your changes are staged, you can push them to the repository. They're now safe and living in the cloud.  Keep in mind that most of our projects are public and other people can see your code.  Never never ever ever please do not push settings_secret.py files or files with API keys, or other sensitive information.  Add all such files to `.gitignore`. They won't be tracked, and better yet, they'll never end up on the web.  People crawl GitHub for passwords and any sneaky ways to turn you project into a crypto-mining, spam sending, toxic malware festival.  Cleaning up a worm-infested meltdown is no fun.      

---

```git merge```
Let's say I added a new feature in the `ajanco` branch and they're ready to add to the project's code base. I'd switch back to master with `git checkout master` and then pull my changes from other branch with `git merge ajanco`. Alternatively, I can go to the project's GitHub page, click "Pull requests" and "New Pull Request."
   
In many projects, someone will be notified and inspect your new code.  You'll get comments back and it's a nice way to chit-chat about our work.  Once approved the code enters the master branch and will be deployed shortly.   

---

## further reading

[try.github.io](https://try.github.io/)

[Git Branching - Basic Branching and Merging](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)

[The seven rules of a great Git commit message](https://chris.beams.io/posts/git-commit/)

