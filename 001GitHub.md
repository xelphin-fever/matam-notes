# GitHub

## General
GIT is a Version Control System

- fancy save button; keeps a journal of saves of files;
keeps previous versions [couple saves back]
- can compare versions visually; shows changes with highlights/colors
- collaborate with other members

### How It Works

<details>
<summary>Repository</summary>

- Repository is shared with all team members
- Database of changes
- Has all versions of project
</details>

<details>
<summary>Personal Copy of Work</summary>

- Can edit without affecting repo
- When done, can commit changes to repo (changes repo)
</details>

<details>
<summary>Centralized VCS</summary>

Centralized VCS
- One server (like big computer everyone can access) all users depend on
- If server becomes corrupted, you lose everything
- can only access with internet
</details>

<details>
<summary>Distributed VCS</summary>

- Each user has a copy of the repo on their computer/server
- Therefore, there are a number of steps all users need to do:
- You pull the main repo to your computer
- You change the repo on your computer (personal copy of work)
- Once finished something, user can commit work (doesn’t change main repo, only saves change [and logs change] in user’s server’s repo)
- Once you want to share changes with others you push the changes

- (Everyone has repo on their server and working copy)
- (Don’t need internet)
- (Can see what different servers do)

</details>

## How To Basics

### Command Line

All git commands start with:

$ ```git```

### States

**Working**: Edit project here. Can send selected files to Staging using add.

**Staging**: Holds all the files that I want to be updated in repo.
Can send to repo using commit.

**Repository (.git directory)**: Holds current project

**Untracked**: If created/changed  files and haven’t even staged them,
then they are untracked by git.

### Steps - Example

- $ ```cd myDirectory```
- $ ```git init``` 
  - Initialize new repository
- $ ```git status```
  - Show status of local repository
- \> ```No commits yet```


- $ ```touch hello.txt``` (create txt file named hello)
- $ ```touch meet.txt``` (create txt file named meet)
- $ ```touch goodbye.txt``` (create txt file named goodbye)
  - (status: all three files are untracked -> shows in red if you do $ ```git status```)
- $ ```git add hello.txt meet.txt``` (add hello.txt and add meet.txt to staging)
  - (status of hello and meet are staged, goodbye is untracked)
- $ ```git commit -m"I say hello and meet person"``` (commit files in staging to repo and add message to commit: text inside “...”)
- [inside hello.txt, change some text]
  - Now the status of hello.txt is modified (red)
- $ ```git add *``` (add all files to staging)
  - Status: hello.txt and goodbye.txt are in staging
- $ ```git commit -m”Full Meeting”``` (commit hello and goodbye [in staging]  to repo)

## Branching

<details>
  <summary>Branching Example</summary>

So imagine the following, you have a project and every
-> is a different commit (saved a new repo version)

**Version 1 (master) (HEAD)**

- $ ```git commit```

Version 1 **<- Version 2 (master)** (HEAD)

- $ ```git commit```

Version 1 <- Version 2 **<-  Version 3 (master)** (HEAD)

- $ ```git branch Task1``` (create branch called Task1)

Version 1 <- Version 2 <-  Version 3 (master) (HEAD) **(Task1)**

- $ ```git checkout Task1``` (move HEAD (pointer to commit from version) to Task1 )

Version 1 <- Version 2 <-  Version 3 (master) (Task1) **(HEAD)**

- $ ```git commit```

Version 1 <- Version 2 <-  Version 3 (master) **<-  Version 3.1  (Task1)** (HEAD)

- $ ```git checkout master```

Version 1 <- Version 2 <-  Version 3 (master) **(HEAD)** <-  Version 3.1  (Task1)

- $ ```git commit```

Version 1 <- Version 2 <-  Version 3 <-  Version 3.1  (Task1)

**<-  Version 3.2   (master) (HEAD)**

- $ ```git commit```

Version 1 <- Version 2 <-  Version 3 <-  Version 3.1  (Task1)

<-  Version 3.2   **<-  Version 4.2(master)** (HEAD)

- $ ```git checkout Task1```

Version 1 <- Version 2 <-  Version 3 <-  Version 3.1  (Task1) **(HEAD)**

<-  Version 3.2   <-  Version 4.2(master)

- $ ```git commit```

Version 1 <- Version 2 <-  Version 3 <-  Version 3.1   **<-  Version 4.1(Task1)** (HEAD)

<-  Version 3.2   <-  Version 4.2(master) 

</details>

### Merge

<details>
  <summary>Merge Example</summary>

- $ ```git checkout master```

Version 1 <- Version 2 <-  Version 3 <-  Version 3.1   <-  Version 4.1(Task1)

<-  Version 3.2   <-  Version 4.2(master) (HEAD)

- $ ```git merge Task1``` (merges between master and Task1, new Version
has changes of both master and Task1)

Version 1 <- Version 2 <-  Version 3 <-  Version 3.1   <-  Version 4.1(Task1)

<-  Version 3.2   <-  Version 4.2

<-Version 5 (HEAD) (master)

- $ ```git checkout -b Task2``` (creates new branch and HEAD points at it)

Version 1 <- Version 2 <-  Version 3 <-  Version 3.1   <-  Version 4.1(Task1)

<-  Version 3.2   <-  Version 4.2

<-Version 5 (HEAD) (master)(Task2)


- $ ```git commit```

Version 1 <- Version 2 <-  Version 3 <-  Version 3.1   <-  Version 4.1(Task1)

<-  Version 3.2   <-  Version 4.2

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<-Version 5 (master) <- Version 6 (HEAD) (Task2)

- $ ```git merge Task2``` (no need for another commit in this case)

Version 1 <- Version 2 <-  Version 3 <-  Version 3.1   <-  Version 4.1(Task1)

<-  Version 3.2   <-  Version 4.2

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<-Version 5 <- Version 6 (HEAD) (master) (Task2)

</details>


### TreeBase

<details>
  <summary>Treebase Example</summary>

Version 1 <- Version 2 <-  Version 3 <-  Version4   <-  Version 5 <-  Version 6 (task1) (HEAD)

<-  Version 4.2   <-  Version 5.2 (master)

- You should try and make sure that your main branch is always functional.
You want to branch only from functional branches not from buggy ones.
So you shouldn’t really directly work directly from the master branch.


- $ ```git rebase master``` (adds branch on top of master -- task1 changed but master didn’t)

Version 1 <- Version 2 <-  Version 3 <-  Version 4.2   <-  Version 5.2 (master) <-  Version4   <-  Version 5 <-  Version 6 (HEAD) (task1)

- Say you’re working on task1, master got updated and has new features you want to use
those features but task1 isn’t completed yet, you can rebase on top of master == use
the features, keep master the same (not appending task1)


- $ ```git checkout master```
- $ ```git merge task1```

Version 1 <- Version 2 <-  Version 3 <-  Version 4.2   <-  Version 5.2 (master) <-  Version4   <-  Version 5 <-  Version 6 (HEAD) (master) (task1)
</details>

## Push Pull

REMOTE: Version 1

LOCAL: Version 1(origin/master) <- Version 2 <-  Version 3 (master) (HEAD)

- $ ```git push``` (updates remote repo to that of master on local repo)

REMOTE: Version 1 <- Version 2 <-  Version 3 (master) (HEAD)


LOCAL: Version 1 <- Version 2 <-  Version 3 (master) (HEAD) (origin/master)

- $ ```git pull``` (pulls current repo from Remote to Local)