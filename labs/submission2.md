# Lab2

## Task 1


### Outputs from terminal

<details>
<summary>Output</summary>

```sh
platon@arch ~/D/DevOps-Intro (main)> git log --oneline -3
f98c674 (HEAD -> main) chore: add test file
ac316a7 (origin/main, origin/feature/lab1, origin/HEAD, feature/lab1) docs(submission1.md): add task2 proofs
0763882 docs(submission1.md): add task2
platon@arch ~/D/DevOps-Intro (main)> git cat-file -p f98c674
tree 209296c6dd01bc86ecacc4e62d3dfdb5750ab716
parent ac316a7816b62cdddbd7d32729b5112eff61deb8
author Platon U. <revlze@yahoo.com> 1770797024 +0300
committer Platon U. <revlze@yahoo.com> 1770797024 +0300
gpgsig -----BEGIN SSH SIGNATURE-----
 U1NIU0lHAAAAAQAAADMAAAALc3NoLWVkMjU1MTkAAAAgnLrvPmJtc1KnCYWG1RuJdtDzLJ
 ABmeZefbw5NoH1Nj0AAAADZ2l0AAAAAAAAAAZzaGE1MTIAAABTAAAAC3NzaC1lZDI1NTE5
 AAAAQMHaHsbT8qblMtZYoKuQtvgOfOtsSuYB8k8ysYPInSOsH5N2g8E2XS4nGfyfCGH67w
 9pvBrD43AhxQQ0fd5FUAw=
 -----END SSH SIGNATURE-----

chore: add test file
platon@arch ~/D/DevOps-Intro (main)> git cat-file -p 209296c6dd01bc86ecacc4e62d3dfdb5750ab716
040000 tree e17290e5ed9e98452e0563ed37f3f36cbe8138bd    .github
100644 blob 6e60bebec0724892a7c82c52183d0a7b467cb6bb    README.md
040000 tree a1061247fd38ef2a568735939f86af7b1000f83c    app
040000 tree cb32363119d52d7a1d2b8974bdc8890c5ff7ad05    images
040000 tree 182b748e8fc19a10326e6c8aba98bdf84791adbd    labs
040000 tree d3fb3722b7a867a83efde73c57c49b5ab3e62c63    lectures
100644 blob 2eec599a1130d2ff231309bb776d1989b97c6ab2    test.txt
platon@arch ~/D/DevOps-Intro (main)> git cat-file -p 2eec599a1130d2ff231309bb776d1989b97c6ab2
Test content
```

</details>

### Explanation of what each object type represents
`Blob`: show raw content of file

`Tree`: it's "directory" -- list of blobs and other trees with permissions and names of files

`Commit`: it's pointer which show -- tree+author+message+link to parent

### Analysis of how Git stores repository data

Git stores a full snapshot of the repo for each commit, not diffs. But identicaly content stored only once -- if the file hasn't changed, the commit's tree simply references the existing blob


## Task 2

### Outputs from terminal

<details>
<summary>Output</summary>

```sh
platon@arch ~/D/DevOps-Intro (main)> git switch -c git-reset-practice
                                     echo "First commit" > file.txt && git add file.txt && git commit -m "First commit"
                                     echo "Second commit" >> file.txt && git add file.txt && git commit -m "Second commit"
                                     echo "Third commit"  >> file.txt && git add file.txt && git commit -m "Third commit"
Switched to a new branch 'git-reset-practice'
[git-reset-practice 9931ac0] First commit
 1 file changed, 1 insertion(+)
 create mode 100644 file.txt
[git-reset-practice 182ed31] Second commit
 1 file changed, 1 insertion(+)
[git-reset-practice e15aeb8] Third commit
 1 file changed, 1 insertion(+)
platon@arch ~/D/DevOps-Intro (git-reset-practice)> git reset --soft HEAD^
platon@arch ~/D/DevOps-Intro (git-reset-practice)> git log --oneline -3
98e89c0 (HEAD -> git-reset-practice) Second commit
e134d25 First commit
f98c674 (main) chore: add test file
platon@arch ~/D/DevOps-Intro (git-reset-practice)> git reset --hard HEAD^
HEAD is now at e134d25 First commit
platon@arch ~/D/DevOps-Intro (git-reset-practice)> git log --oneline -3
e134d25 (HEAD -> git-reset-practice) First commit
f98c674 (main) chore: add test file
ac316a7 (origin/main, origin/feature/lab1, origin/HEAD, feature/lab1) docs(submission1.md): add task2 proofs
platon@arch ~/D/DevOps-Intro (git-reset-practice)> git reflog
e134d25 (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD^
98e89c0 HEAD@{1}: reset: moving to HEAD^
90a5679 HEAD@{2}: commit: Third commit
98e89c0 HEAD@{3}: commit: Second commit
e134d25 (HEAD -> git-reset-practice) HEAD@{4}: commit: First commit
f98c674 (main) HEAD@{5}: checkout: moving from main to git-reset-practice
f98c674 (main) HEAD@{6}: commit: chore: add test file
ac316a7 (origin/main, origin/feature/lab1, origin/HEAD, feature/lab1) HEAD@{7}: pull origin feature/lab1: Fast-forward
3b71c57 HEAD@{8}: checkout: moving from feature/lab1 to main
ac316a7 (origin/main, origin/feature/lab1, origin/HEAD, feature/lab1) HEAD@{9}: commit: docs(submission1.md): add task2 proofs
0763882 HEAD@{10}: commit: docs(submission1.md): add task2
3b71c57 HEAD@{11}: checkout: moving from main to feature/lab1
3b71c57 HEAD@{12}: commit: chore: add PR template
839a326 HEAD@{13}: checkout: moving from feature/lab1 to main
839a326 HEAD@{14}: checkout: moving from main to feature/lab1
839a326 HEAD@{15}: commit: docs: add second proof(screenshot with **Verified**)
002455b HEAD@{16}: commit: docs: add commit signing summary
d6b6a03 HEAD@{17}: clone: from github.com:revlze/DevOps-Intro.git
platon@arch ~/D/DevOps-Intro (git-reset-practice)> git reset --hard 90a5679
HEAD is now at 90a5679 Third commit
platon@arch ~/D/DevOps-Intro (git-reset-practice)> git log --oneline -3
90a5679 (HEAD -> git-reset-practice) Third commit
98e89c0 Second commit
e134d25 First commit
platon@arch ~/D/DevOps-Intro (git-reset-practice)> 
```
</details>

### What changed in the working tree, index, and history for each reset

`git reset --soft HEAD^`: HEAD moved from Third to Second commit. Working tree and index untouched -- Third commit changes stayed staged (ready to commit again). History lost Third commit from `git log`.

`git reset --hard HEAD^`: HEAD moved from Second to First commit. Working tree and index both wiped -- Second commit changes gone from disk. History lost Second commit from `git log`. File `file.txt` now only contains "First commit".

### Analysis of recovery process using reflog

After both resets, `git log` shows only First commit -- Second and Third are "gone". But `git reflog` still tracks every HEAD movement:
```
90a5679 HEAD@{2}: commit: Third commit
98e89c0 HEAD@{3}: commit: Second commit
```

Ran `git reset --hard 90a5679` to recover all three commits. `git log` now shows First → Second → Third again.

## Task 3

### Output from terminal

<details>
<summary>Output</summary>

```sh
platon@arch ~/D/DevOps-Intro (main)> git switch -c side-branch
Switched to a new branch 'side-branch'
platon@arch ~/D/DevOps-Intro (side-branch)> echo "Branch commit" >> history.txt
platon@arch ~/D/DevOps-Intro (side-branch)> git add history.txt && git commit -m "Side branch commit"
[side-branch cb8397c] Side branch commit
 1 file changed, 1 insertion(+)
 create mode 100644 history.txt
platon@arch ~/D/DevOps-Intro (side-branch)> git switch -
Switched to branch 'main'
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)
platon@arch ~/D/DevOps-Intro (main)> echo "Main commit" >> main.txt
platon@arch ~/D/DevOps-Intro (main)> git add main.txt && git commit -m "Main branch commit"
[main 87da990] Main branch commit
 1 file changed, 1 insertion(+)
 create mode 100644 main.txt
platon@arch ~/D/DevOps-Intro (main)> git log --oneline --graph --all
* 87da990 (HEAD -> main) Main branch commit
| * cb8397c (side-branch) Side branch commit
|/  
* f98c674 chore: add test file
* ac316a7 (origin/main, origin/feature/lab1, origin/HEAD, feature/lab1) docs(submission1.md): add task2 proofs
* 0763882 docs(submission1.md): add task2
* 3b71c57 chore: add PR template
* 839a326 docs: add second proof(screenshot with **Verified**)
* 002455b docs: add commit signing summary
* d6b6a03 Update lab2
* 87810a0 feat: remove old Exam Exemption Policy
* 1e1c32b feat: update structure
* 6c27ee7 feat: publish lecs 9 & 10
* 1826c36 feat: update lab7
* 3049f08 feat: publish lec8
* da8f635 feat: introduce all labs and revised structure
* 04b174e feat: publish lab and lec #5
* 67f12f1 feat: publish labs 4&5, revise others
* 82d1989 feat: publish lab3 and lec3
* 3f80c83 feat: publish lec2
* 499f2ba feat: publish lab2
* af0da89 feat: update lab1
* 74a8c27 Publish lab1
* f0485c0 Publish lec1
* 31dd11b Publish README.md
```
</details>

<details>
<summary>Output `git log --all --oneline`</summary>

```sh
platon@arch ~/D/DevOps-Intro (main)> git log --all --oneline
87da990 (HEAD -> main) Main branch commit
cb8397c (side-branch) Side branch commit
f98c674 chore: add test file
ac316a7 (origin/main, origin/feature/lab1, origin/HEAD, feature/lab1) docs(submission1.md): add task2 proofs
0763882 docs(submission1.md): add task2
3b71c57 chore: add PR template
839a326 docs: add second proof(screenshot with **Verified**)
002455b docs: add commit signing summary
d6b6a03 Update lab2
87810a0 feat: remove old Exam Exemption Policy
1e1c32b feat: update structure
6c27ee7 feat: publish lecs 9 & 10
1826c36 feat: update lab7
3049f08 feat: publish lec8
da8f635 feat: introduce all labs and revised structure
04b174e feat: publish lab and lec #5
67f12f1 feat: publish labs 4&5, revise others
82d1989 feat: publish lab3 and lec3
3f80c83 feat: publish lec2
499f2ba feat: publish lab2
af0da89 feat: update lab1
74a8c27 Publish lab1
f0485c0 Publish lec1
31dd11b Publish README.md
```

</details>

### Reflection on how the graph aids understanding
The graph shows where each branch points and how commits relate to each other -- makes it easy to spot diverged branches, merges, and parallel work instead of reading simple log output.



## Task 4

### Output terminal

```sh
platon@arch ~/D/DevOps-Intro (main)> git tag v1.0.0
platon@arch ~/D/DevOps-Intro (main)> git push origin v1.0.0
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To github.com:revlze/DevOps-Intro.git
 * [new tag]         v1.0.0 -> v1.0.0
```

### Tag and associated commit

| Tag      | Commit hash | Message                              |
| -------- | ----------- | ------------------------------------ |
| `v1.0.0` | `ac316a7`   | docs(submission1.md): add task2 proofs |

### Why tags matter

Tags pin a human-readable version label to an exact commit, which is essential for release management. CI/CD pipelines often trigger builds and deployments on tag pushes (e.g. `v*`), and tags serve as anchors for generating changelogs and release notes.

## Task 5

### git switch (modern — branch switching)

```sh
platon@arch ~/D/DevOps-Intro (main)> git switch -c cmd-compare
Switched to a new branch 'cmd-compare'
platon@arch ~/D/DevOps-Intro (cmd-compare)> git switch -
Switched to branch 'main'
```

### git checkout (legacy — overloaded)

```sh
platon@arch ~/D/DevOps-Intro (main)> git checkout -b cmd-compare-2
Switched to a new branch 'cmd-compare-2'
platon@arch ~/D/DevOps-Intro (cmd-compare-2)> git status
On branch cmd-compare-2
Untracked files:
  (use "git add <file>..." to include in what will be committed)
    labs/submission2.md

nothing added to commit but untracked files present (use "git add" to track)
platon@arch ~/D/DevOps-Intro (cmd-compare-2)> git branch
  cmd-compare
* cmd-compare-2
  feature/lab1
  main
  side-branch
```

### git restore (modern — file operations)

```sh
platon@arch ~/D/DevOps-Intro (main)> echo "scratch" >> demo.txt
platon@arch ~/D/DevOps-Intro (main)> git status
Changes not staged for commit:
    modified:   demo.txt
platon@arch ~/D/DevOps-Intro (main)> git restore demo.txt
platon@arch ~/D/DevOps-Intro (main)> git status
nothing added to commit but untracked files present

platon@arch ~/D/DevOps-Intro (main)> echo "scratch" >> demo.txt
platon@arch ~/D/DevOps-Intro (main)> git add demo.txt
platon@arch ~/D/DevOps-Intro (main)> git status
Changes to be committed:
    modified:   demo.txt
platon@arch ~/D/DevOps-Intro (main)> git restore --staged demo.txt
platon@arch ~/D/DevOps-Intro (main)> git status
Changes not staged for commit:
    modified:   demo.txt

platon@arch ~/D/DevOps-Intro (main)> git restore --source=HEAD^ demo.txt
platon@arch ~/D/DevOps-Intro (main)> git status
Changes not staged for commit:
    deleted:    demo.txt
```

### When to use each command

`git switch` — use for branch operations only: creating, switching, toggling between branches. It's focused and won't accidentally touch files.

`git checkout` — legacy command that handles both branches (`-b`) and files (`-- <file>`). Still works, but its dual purpose makes it confusing and error-prone. Avoid in new workflows.

`git restore` — use for file operations only: discarding working tree changes, unstaging files (`--staged`), or restoring a file from another commit (`--source`). It replaced the ambiguous `git checkout -- <file>` syntax.

## Task 6

### GitHub Community

Starring a repo bookmarks it and signals appreciation to maintainers -- high star count boosts project visibility, attracts contributors, and serves as a trust indicator in the open-source ecosystem.

Following developers keeps their activity (commits, new repos, stars) in your feed, which helps stay in sync with teammates during projects and exposes you to new tools and patterns from experienced engineers.

