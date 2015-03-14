<h1>Git Basics</h1>
<h2>1: Installing Git (tbd)</h2>
<p> </p>
<h2>2: Committing</h2>
<p>Committing means saving your work (to your local version of git).  The commands you will be using are</p>
<ol>
  <li>git status</li>
  <li>
    <p>(<em>optional</em>) git checkout -- &lt;file name&gt;</p>
  </li>
  <li>(<em>optional</em>) git rm --cached &lt;file name&gt;</li>
  <li>(<em>optional</em>) git add &lt;file name&gt;</li>
  <li>git commit -am '&lt;description of change&gt;'</li>
</ol>
<p>Lets go over these in more detail.</p>
<h3>git status</h3>
<p>The first step is to use git status to see where you are at in your work.  This will show you files in three categories.</p>
<ol>
  <li>The first category is new files that will be added to git when you commit.</li>
  <li>The second is files that are already in git but have been modified, when you call 'git commit' (with the -a flag) those changes will be saved.</li>
  <li>The third category is files under your git directory that will not be save to git such as work and build directories or .tmp or .swp files.</li>
</ol>
<p>
  <img src="https://github.com/NyckJohnson/HowToGit/blob/master/imgs/status.png"/>
</p>
<h3>git add &lt;file&gt;</h3>
<p>If there are any files in the third category (those not being saved) which you want to add to git, this will add them.  Be careful however because if you designate a directory it will include all subfiles, you may not want all of them.  Best to run git status again after doing this.</p>
<p>
  ![alt tag](https://raw.githubusercontent.com/NyckJohnson/HowToGit/master/imgs/add.png)
</p>
<h3>git checkout -- &lt;file&gt;</h3>
<p>This will revert a file to its last committed version.  If you do not want to save the changes that where made to it.</p>
<h3>git rm --cached &lt;file&gt;</h3>
<p>If there are files in the second category you do not want to save in git you can remove them from git with this command.</p>
<p>
  ![alt tag](https://raw.githubusercontent.com/NyckJohnson/HowToGit/master/imgs/cached.png)
</p>
<p>The "–cached" is important, it means that you are removing the file from git but not from your hard drive.  You are moving it to the untracked files list.  Without "–cached" this command will delete the file from your harddrive.</p>
<p>This can also be used to remove files that are already saved to git but you no longer want to track.</p>
<h3>git commit -am 'some description of what is changed'</h3>
<p>This saves all of the changes you have made to git.</p>
<p>For your curiosity</p>
<ol>
  <li>The -a flag means to do 'git add' to each of the modified files (those in category two in git status) so that they will be saved. </li>
  <li>The -m flag includes the message which describes what the changes are.  Using git without this opens your preferred text editor automatically to take that message which can sometimes lead to problems.</li>
</ol>
<p>
  ![alt tag](https://raw.githubusercontent.com/NyckJohnson/HowToGit/master/imgs/commit.png)
</p>
<h2>3: Pushing</h2>
<p>Once you have commits saved to the your local version of git and are ready to share your changes you need to push them to the Solution Teams origin copy of git.</p>
<p>The steps for that are as follows:</p>
<ol>
  <li>git status (<em>just like above its best to make sure of what you are about to do</em>)</li>
  <li>git pull --rebase</li>
  <li>(<em>optional</em>) git mergetool</li>
  <li>git push</li>
</ol>
<h3>git pull --rebase</h3>
<p> git pull takes grabs the teams master copy with whatever changes the rest of the team has made and copies it to your local git, then it takes your changes and adds them in.</p>
<p>
  ![alt tag](https://raw.githubusercontent.com/NyckJohnson/HowToGit/master/imgs/pull.png)
</p>
<p>the --rebase makes it so that if anyone goes through and reads log of changes it will appear much cleaner for them.</p>
<h3>git mergetool</h3>
<p>This is covered in part 4 "Merge Conflicts".</p>
<h3>git push</h3>
<p>
  ![alt tag](https://raw.githubusercontent.com/NyckJohnson/HowToGit/master/imgs/push.png)
</p>
<p>Git push, this takes your local version of git and copies it to the teams master, where we all can get it.</p>
<p>Our build server pulls this every day before running its test and then pushes it to vault so within 24hrs your changes should be pushed.</p>
<p> </p>
<h2>4: Merge Conflicts (tbd)</h2>
<p>When you pull, all of the changes that other team members have pushed get brought down to your local master, then your changes are added to them.  Git is pretty good at combining changes in a sane fashion BUT; if both you and another team member changed the same line in a file, git will ask you to resolve the problem yourself rather than guess who was right.</p>
<h3>git mergetool</h3>
<h3>setting up mergetool -&gt; ?????</h3>
<h1>Advanced Topic- Branches (in progress)</h1>
<p>Often we work on many projects at once, not finishing one before starting the next.  When we finish one we want to load it's changes up to Origin but we don't want to push the other changes we made to half complete projects.  This is what branches are for.  In the same way that your local Master is a version of the teams Origin.  A branch is a version of your Master.  You can create a branch make some changes there, save them in a commit and then move to a different branch to work on it's project.</p>
<h2>switching between branches</h2>
<ol>
  <li>git checkout &lt;branch_name&gt;</li>
</ol>
<p>If you are on a branch (including master) with unsaved changes, it will warn you to commit your work before switching</p>
<h2>create branch</h2>
<ol>
  <li>git status</li>
  <li>git checkout -b &lt;branch_name&gt;</li>
</ol>
<p>You want to call this while you are on Master and not on another branch.  Otherwise you are branching off a branch and getting confused down the road.</p>
<p>The '-b' means you are create a new branch instead of switching</p>
<h2>save branch</h2>
<p>This is just like committing anywhere else.</p>
<ol>
  <li>git status</li>
  <li>git commit -am "&lt;message&gt;"</li>
</ol>
<h2>merge</h2>
<p>When you are ready to push your project to Origin there are a few more steps to first get it to your master.  A process called merging.</p>
<ol>
  <li>git status</li>
  <li>git commit -am "save"</li>
  <li>git checkout master</li>
  <li>git merge &lt;branc_name&gt; --squash</li>
  <li>git commit -am "message to describe the branch"</li>
</ol>
<p>From this point you can pull and push like normal.</p>
<p> </p>
