git-tfs Workflow
================

Start
-----

Clone an existing TFS project::

    git tfs clone https://server/path $/project

where ``server/path`` is the server location of the project
(but does not the project name itself),
and ``$/project`` is the name of the project.
Alternatively, clone from the last changeset (faster download)::

    git tfs quick-clone https://server/path $project

Automatically handle line endings across operating systems::

    git config core.autocrlf true

Ignore file mode changes::

    git config core.filemode false

Work
----

1. Create a branch to work on a feature (use git normally).
2. Rebase on that branch to cut down the number of commits.
3. Switch to the master branch.
4. Look over Team Explorer (in Visual Studio) to see if anyone
   has make changes to the project you worked on.
5. Fetch the repository and check the log:: 

     git tfs fetch
     git log --all --oneline --graph --decorate

   (Look for ``tfs/default``, which is the remote repository.)

6. Pull the repository::

     git tfs pull

7. Go back to the feature branch.
8. Rebase on the updated master::

     git rebase -i master

9. Do a build/run to make sure script works.
10. Go to the master branch.
11. Merge to master::

     git merge [branch]

12. Delete merged branch::

     git branch -d [branch]

13. Check-in work to TFS::

     git tfs rcheckin

Branches
--------

Create a new TFS branch::

    git tfs branch $/tfvc-test/featureBee

``git-tfs`` will add a changeset in TFS with the new branch,
and it will show up as a new git commit.
``HEAD`` will still be pointing to ``master``,
so create a git branch from the commit that created the TFS branch.
