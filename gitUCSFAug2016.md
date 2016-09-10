##Software Carpentry GIT Crib Sheet
####UCSF Aug.4-5, 2016
####Tim Dennis, UCSD DL 

####Before class:
* set up shell:
	* enlarge text size
	* `export PS1='$ '`
	* `export PROMPT_COMMAND="history 1 >> ~/Dropbox/GitHistory.txt"`
* check software installation for git AND account with GitHub
* need proxy?
* get slides setup
* remind students to register for GitHub account

####Reources
* class website: https://jt14den.github.io/2016-08-04-UCSF-R/
* etherpad: http://pad.software-carpentry.org/ucsf-08-2016

* Git for beginners: http://stackoverflow.com/questions/315911/git-for-beginners-the-definitive-practical-guide 
* fixing detached head: http://stackoverflow.com/questions/10228760/fix-a-git-detached-head (`git checkout master`)
	
####SETUP
**Objectives:** get system set up for proper attribution of your work

* Slides: https://docs.google.com/presentation/d/1CaamfnsLj3XzACwjl9LElnrCu6OrbVHgVBTYNpCi2Ew/edit#slide=id.p
* open shell, can be anywhere
* specify your name, to be recorded in commits
* `git config --global user.name "k8hertweck"`
	* specify your email, to be recorded in commits
* `git config --global user.email "k8hertweck@gmail.com"`
	* specify text editor, to be used in committing
	* nano: `git config --global core.editor "nano -w"`
	* text wrangler: `git config --global core.editor "edit -w"`
	* notepad++: `git config --global core.editor "'c:/program files (x86)/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"`
	* kate: `git config --global core.editor "kate"`
* `--global` means will apply for every command entered afterward
* check settings: `git config –list`
* syntax for git: `git VERB`	

####CREATING A REPO (WORKING LOCALLY)
**Objectives:** start tracking versions in a particular folder/directory (repository)

* start in home directory
* create directory and change directories
```
mkdir planets
cd planets
```

* tell git where to store old records and versions of file


```
git init
```

```
ls
```

* list everything (including hidden files)

```
ls -a
```

* result is a subdirectory with information about project
* if this is removed, we don't have access to versioning anymore
* ask status of project
```
git status
```

* output also adds helpful comments

_On the white board draw a box representing the working area and
 explain that this is where you work and make changes._

* challenge 1
* Because you would create a git nested repo, which
* will be recorded by the parent repo as a gitlink (special entry in the index)
* but whose content would be otherwise ignored
	- As opposed to a submodule (which also records a gitlink, and the submodule url in the parent .gitmodules file), a repo with a nested git repo in it would not be able to get the nested repo content back: all the parent has is a SHA1 in the entries of its index. It does not have the url of the nested repos.
	- Anybody cloning the parent repo would get an "empty folder" for the nested git repo, without being able to find to which other repo this "empty folder" is for.


####TRACKING CHANGES: 
**Objectives:** practice workflow (modify-add-commit), explain where information is stored

* create new file: 

```
nano mars.txt
```

* copy and add text `Cold and dry, but everything is my favorite color` , exit and save, `ls`, `cat mars.txt`
* show status of project: `git status`
	* draw attention to "untracked files": there's something not being tracked
* add file: 

```
git add mars.txt
```

* `git status` draw attention to "Changes to be committed": it's tracking, but the changes aren't recorded

_Now, lets add files that are inside:
On the white board draw a box representing the staging area (index) and
explain that this is where we set up the next snapshot of our project.
**Like a photographer in a studio**, we're putting together a shot
before we actually snap the picture.
Connect the working area box and the staging box with 'git add'._

* commit file: 
```
git commit -m "creating script"
```
	* commits record to history in .git, called a revision, with short identifier
	* run without -m and will open editor to add comment (you've specified your preference earlier today)
	* good commits: brief (<50 characters), for more info, add empty line (adds in separate field)
* `git status`

_On the white board draw a box representing the project history.
Once we take a snapshot of the project that snapshot becomes a permanent reference point in the project's history that we can always go back to.
The history is like a photo album of changes, and each snapshot has a time stamp, the name of the photographer, and a description.
Connect the staging area to the history with `git commit -m "message"`.
In order to save a snapshot of the current state (revision) of the repository, we use the commit command.
This command is always associated with a message describing the changes since the last commit and indicating their purpose.
Git will ask you to add a commit message.
This is just to remind you what changes you made.
Informative commit messages will serve you well someday, so make a habit of never committing changes without at least a full sentence description._

__ADVICE: Commit often__
_In the same way that it is wise to often save a document that you are working on, so too is it wise to save numerous revisions of your code.
More frequent commits increase the granularity of your undo button._

__ADVICE: Good commit messages__
[because it's important!](http://www.commitlogsfromlastnight.com/)
_There are no hard and fast rules, but good commits are atomic: they are the smallest change that remain meaningful.
A good commit message usually contains a one-line description followed by a longer explanation if necessary.
For code, it's useful to commit changes that can be reviewed by someone in under an hour.
Or it can be useful to commit changes that "go together" - for example, one paragraph of a manuscript, or each new function added to your script.
For example, if you work on your code all day long (add 200 lines of code, including 5 new functions and write 7 pages of your new manuscript including deleting an old paragraph), and at 3:00 you make a fatal error or deletion, but you didn't commit once, then you will have a hard time recreating the version you are looking for - because it doesn't exist!_

* check history: 
```
git log
```
	* lists all revisions in reverse chronological order: full identifier (relate to short identifier, same initial characters),
	* when created, log message, show `oneline`
* make another change (this is just one way): 
```
nano mars.txt
```

```
The two moons may be a problem for Wolfman
```

```q
cat mars.txt
```

* check status: `git status`
* look at differences: 

```
git diff
```

1. first line: old and new version of files, similar to diff command in Unix
2. second line: labels for revisions
3. third and fourth: name of file changing
4. last lines: actual changes

commit changes: 

```
git commit -m "adding change"
```

* but change hasn't been added!: git add, git commit
working through staging

```
nano morning.txt
```

make change, 

```
cat morning.txt
```

look at differences: 

```
git diff
```

stage file: 

```
git add morning.txt
git diff #(no output)

git diff –staged  #(shows differences bt staged and head)
git commit -m
git status
git log
git commit workflow
```


*challenges <http://swcarpentry.github.io/git-novice/04-changes/#choosing-a-commit-message>
Answer 1 is not descriptive enough, and answer 2 is too descriptive and redundant, but answer 3 is good: short but descriptive.


####EXPLORING HISTORY
Objectives: identify and use Git commit numbers, compare versions, restore old versions

* compare different versions of commits
* HEAD~1 (HEAD minus 1) and HEAD~2 refer to old commits: 
* most recent end of chain is HEAD

```
git diff HEAD~1 mars.txt
git diff HEAD~2 mars.txt
```

`git log` gives strings of digits and letters the id for the commit: 

```
git diff XXXXXXXX mars.txt
```

* can also just use first few characters: 

```
git diff XXX mars.txt
```

**how to revert to old version?**

* make another change to mars.txt -- delete all and replace with something

```
nano mars.txt
```

```
git status
```

git checkout to remove unstaged changes (default to previous committed version)

```
git checkout HEAD mars.txt
```

* **remember** that you want changes before most recent commit 

challenge

####IGNORING THINGS
Objectives: ignore some files, why ignoring is useful

sometimes backup files are created by other programs, or intermediate files we don't want to track
create dummy files 
```bash
mkdir results 
touch a.dat b.dat c.dat results/a.out results/b.out
git status
```
lots of stuff needs to be committed, but we don't want to include data or output in our repo?  1) good to keep source data as read only and any derived data should be reproducible from code 2) gh has file limits, 3)could overwrite data with collaborators -- output should be regeneratable by code.
```
nano .gitignore 
```

* add *.dat and results/

```
git status
```

now .gitignore is the only thing there! let's add it so our collaborators benefit from it.
```
git add .gitignore
git commit -m “add ignore file”
git status
```

gitignore will prevent us from adding ignored files 

```
git add a.dat: error
```

to see what is ignored run: 

```
git status --ignored
```

####REMOTES IN GITHUB
Objectives: explain why remote repos, clone remote repos, push/pull

#### Github is cool because collaboration!

we've been working in local repo, so we're the only ones who can see our work
GitHub is a remote repo that can be published for other folks to see, use, improve you work. 

1. log in to GitHub, click icon in top right corner, create repo called “planets”
2. resulting page has info about configuring repository, it's done the mkdir planets, cd planets, git init process remotely
3. connect the two repos
4. copy https url to clipboard
5. go to local repo (in shell): 

``` 
git remote add origin https://github.com/k8hertweck/planets
git remote -v
```

* check that it worked
**origin** is a nickname for remote repo
* now send local changes to remote repo: 

```
git push origin master
```
check remote repo, changes should be there.

* On github create README file and add brief comment about the purpose of the materials, 
* commit change, go back to terminal: 

```
git pull origin master
```

**show GITHUB & SWC here? -- issues** 

http://swcarpentry.github.io/git-novice/07-github/#github-gui

https://github.com/hadley/dplyr

http://swcarpentry.github.io/git-novice/07-github/#push-vs-commit

>>Basically git commit "records changes to the repository" while git push "updates remote refs along with associated objects". So the first one is used in connection with your local repository, while the latter one is used to interact with a remote repository.

####COLLABORATING
Objectives: collaborate pushing to common repo

1. pair up students
2. in your planets repo on GitHub, click settings, select collaborators, enter partner's username
3. partner should cd to another directory (Desktop) and make copy of partner's repo: git clone htt#ps://github.com/vlad/planets.git (replace vlad with your partner's name)
4. collaborator should make changes, add, commit, git push origin master
5. original owner can pull changes onto their machine

**challenge** switch roles and repeat 

####CONFLICTS
Objectives: explain when conflicts occur, resolve conflicts from a merge

1. each partner adds a (different) line to mars.txt, adds, commits, pushes to github
2. the second push will fail
3. failed pusher should: 
4. `git pull origin master`
5. reconcile change and remove markers (you can accept the remote or local changes or add something else)
6. git add, status, commit, push
7. other partner can pull without additional changes needing to take place

####COLLABORATION EXERCISE
1. collaboration tool: https://github.com/jt14den/git-collaboration
2. students can fork the repo 
3. explain forking: making own copy of a repo that isn't owned by you
4. make changes to one of the countries
5. submit pull request to original owner


####OPEN SCIENCE
can use version control as electronic lab notebook for computational work
more open means more citation and reuse

####HOSTING
where to put code and data?
can do this yourself by purchasing domain and paying ISP to host
can also use public service
includes web interface, plus other functionalities: ability to collaborate, get DOI, academic folks can get free private repos for education 

####LICENSING
adding license and citation info
choosing licenses
licensing vs. social expectations

####WRAPPING UP
sticky notes for summary
link to materials on GitHub: http://software-carpentry.org/lessons.html 
reminders about hosting other workshops, becoming an instructor
