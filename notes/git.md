<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#orgheadline39">1. GIT Summary</a>
<ul>
<li><a href="#orgheadline16">1.1. Fundamental</a>
<ul>
<li><a href="#orgheadline6">1.1.1. Objects</a></li>
<li><a href="#orgheadline12">1.1.2. File Structure</a></li>
<li><a href="#orgheadline15">1.1.3. Git's Three Role</a></li>
</ul>
</li>
<li><a href="#orgheadline38">1.2. Basic Command</a>
<ul>
<li><a href="#orgheadline18">1.2.1. Server</a></li>
<li><a href="#orgheadline37">1.2.2. Local</a></li>
</ul>
</li>
</ul>
</li>
</ul>
</div>
</div>

# GIT Summary<a id="orgheadline39"></a>

## Fundamental<a id="orgheadline16"></a>

### Objects<a id="orgheadline6"></a>

Objects are saved in <span class="underline">$GIT<sub>HOME</sub>/objects</span>
Objects are hashed with SHA1 algorithm.

1.  Types

    Has 4 types

        git cat-file -p (<Object>|<Hash>) #cmd to inspect contents
        git cat-file -s (<Object>|<Hash>) #cmd to inspect size
        git cat-file -t (<Object>|<Hash>) #cmd to inspect type

    1.  Blob

        Zipped content file

    2.  Tree

        Contents

        ---

        100644 blob 5ec586d228b5ff1e8c845c4ed8c2d01f3a159b24    README.md

        040000 tree d68e3ec28541c04deef65

    3.  Commit

        Contents

        ---

        tree 53b61d1e46b9886ad7d92b305108e18afe244e2a

        parent 8c181c56a840e380bef7925246b6f626ac76c596

        author Daniel Choi <danielc@ibsglobalweb.com> 1448157452 +1100

        committer Daniel Choi <danielc@ibsglobalweb.com> 1448157452 +1100

        add a ruby file

    4.  Tags

        Almost same as Commit but immutable

### File Structure<a id="orgheadline12"></a>

1.  configuration file

    `$GIT_HOME/config`

2.  references

    local: `$GIT_HOME/refs/heads/{BRANCH|TAG}`
    remote: `$GIT_HOME/refs/remotes/$REMOTE_NAME/{BRANCH|TAG}`

3.  Objects

    `$GIT_HOME/objects`

4.  HEAD

    last commit and next parent
    `$GIT_HOME/HEAD`

5.  FETCH<sub>HEAD</sub>

    Containing all remote branches and tags info

### Git's Three Role<a id="orgheadline15"></a>

I have been confused with these role.
`git status` returns the result of comparison of these roles
`git ls-files` returns the list of `Index` files

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">Role</th>
<th scope="col" class="org-left">Description</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">Working Directory</td>
<td class="org-left">sandbox</td>
</tr>


<tr>
<td class="org-left">Index</td>
<td class="org-left">proposed next commit snapshot</td>
</tr>


<tr>
<td class="org-left">HEAD</td>
<td class="org-left">last commit snapshot, next parent</td>
</tr>
</tbody>
</table>

1.  Working Directory

2.  Index

## Basic Command<a id="orgheadline38"></a>

### Server<a id="orgheadline18"></a>

1.  Create Bare Repository

        git init --bare <DIR_NAME> #e.g. git -init --bare dummy-server.git

### Local<a id="orgheadline37"></a>

1.  Clone Repository

    Multiple protocols are supported like file, http, ssh, git

        git clone <Server URL> # e.g git clone ~/dev/dummy-git-server

2.  .gitignore file

        # no .a files
        *.a
        # but do track lib.a, even though you're ignoring .a files above
        !lib.a # ! is negate
        # only ignore the TODO file in the current directory, not subdir/TODO
        /TODO
        # ignore all files in the build/ directory
        build/
        # ignore doc/notes.txt, but not doc/server/arch.txt
        doc/*.txt
        # ignore all .pdf files in the doc/ directory
        doc/**/*.pdf

3.  git add

        git add (files)
        git add .

4.  git status

        git status -s # Short Description

5.  git diff

        git diff          # working dir vs index
        git diff --staged # index vs head

6.  git commit

        git commit -m         # with message
        git commit -a         # skipping staging
        git commit --amend    # reword last commit

7.  git rm

        git rm --cached (files) # remove it from your staging area
        git rm log/\*.log       # file-glob pattern

8.  git mv

        git mv file_from file_to
        git rm log/\*.log       # file-glob pattern

9.  git log

        ####
        # shows the di erence intro- duced in each commit
        ####
        git log -p -2
        # -2, which limits the output to only the last two entries:
        # diff --git a/lib/simplegit.rb b/lib/simplegit.rb
        # index a0a60ae..47c6340 100644
        # --- a/lib/simplegit.rb
        # +++ b/lib/simplegit.rb
        # @@ -18,8 +18,3 @@ class SimpleGit
        # end
        # end -
        # -if $0 == __FILE__
        # -  git = SimpleGit.new
        # -  puts git.show
        # -end

        ####
        # prints below each commit entry a list of modified files, how many files were changed
        ####
        git log --stat
        # README           |  6 ++++++
        # Rakefile         | 23 +++++++++++++++++++++++
        # lib/simplegit.rb | 25 +++++++++++++++++++++++++
        #  3 files changed, 54 insertions(+)

        ####
        # changes the log out- put to formats other than the default
        ####
        git log --pretty=online
        # ca82a6dff817ec66f44342007202690a93763949 changed the version number
        # 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7 removed unnecessary test
        # a11bef06a3f659402fe7563abf99ad00de2209e6 first commit

        git log --pretty=format:"%h - %an, %ar : %s"
        # ca82a6d - Scott Chacon, 6 years ago : changed the version number
        # 085bb3b - Scott Chacon, 6 years ago : removed unnecessary test
        # a11bef0 - Scott Chacon, 6 years ago : first commit

        ####
        # adds a nice little ASCII graph showing your branch and merge history
        ####
        git log --pretty=format:"%h %s" --graph
        # * 2d3acf9 ignore errors from SIGCHLD on trap
        # * 5e3ee11 Merge branch 'master' of git://github.com/dustin/grit
        # |\
        # | * 420eac9 Added a method for getting the current branch.
        # * | 30e367c timeout code and tests

10. git log, limiting output

        git log --pretty="%h - %s" --author=gitster --since="2008-10-01" \
            --before="2008-11-01" --no-merges
        # 5610e3b - Fix testcase failure when extended attributes are in use
        # acd3b9e - Enhance hold_lock_file_for_{update,append}() API
        # f563754 - demonstrate breakage of detached checkout with symbolic link HEAD
        # d1a43f2 - reset --hard/read-tree --reset -u: remove unmerged new paths
        # 51a94af - Fix "checkout --track -b newbranch" on detached HEAD
        # b0ad11e - pull: allow "git pull origin $something:$current_branch" into an unborn branch

11. git remote

    Default Remote name is 'origin'

        ####
        # show all remotes
        ####
        git remote -v
        # origin https://github.com/schacon/ticgit (fetch)
        # origin https://github.com/schacon/ticgit (push)

        ####
        # add a remote
        ####
        git remate add <Remote Name> <Server URL>

        ####
        # inspect remote
        ####
        git remote show origin
        # * remote origin
        #   Fetch URL: https://github.com/schacon/ticgit
        #   Push  URL: https://github.com/schacon/ticgit
        #   HEAD branch: master
        #   Remote branches:
        #   master                               tracked
        #   dev-branch                           tracked
        #   Local branch configured for 'git pull':
        #   master merges with remote master
        #   Local ref configured for 'git push':
        #       master pushes to master (up to date)

        ####
        # rename remote
        ####
        git remote rename <name_from> <name_to>

12. git fetch

13. git branch

        git branch -v
        # iss53 93b412c fix javascript issue
        # * master  7a98805 Merge branch 'iss53'
        # testing 782

        ####
        # --merged and --no-merged options can filter this list to branches that you have or
        # have not yet merged into the branch you’re currently on.
        ####
        git branch --merged
        # iss53
        # * master

        git branch --no-merged
        # testing

        ####
        # delete branch
        ####
        git branch -d <Branch Name>

        ####
        # setup stream
        ####
        git branch -u(--set-upstream-to) origin/serverfix

14. git merge

15. git pull

    in general fetch+merge

16. git push

17. git reset

18. git checkout

    Used to copy files from the history (or stage) to the working directory, and to optionally switch branches.

        git checkout <POINT> (files)

        ####
        # create new brach and checkout
        ####
        git checkout -b <New Branch Name>
