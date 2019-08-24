
# GIT

## fetch vs pull
git **fetch** really only downloads new data from a remote repository - but it doesn't integrate any of this new data into your working files. Fetch is great for getting a fresh view on all the things that happened in a remote repository.

git **pull**, update your current HEAD branch with the latest changes from the remote server. This means that pull not only downloads new data; it also directly integrates it into your current working copy files. 

    git pull = git fetch + git merge


## merge vs rebase 
git rebase is that it solves the same problem as git merge. Both of these commands are designed to integrate changes from one branch into another branch—they just do it in very different ways.

**Merge preserves history whereas rebase rewrites it.**

Example:

Suppose originally there were 3 commits, A, B, C:

    master  : A  B  C
    feature :

Then developer Dan created commit D, and developer Ed created commit E:

    master  : A  B  C  D
    feature :         E

#### Merge:
git checkout feature
git merge master

    master  : A  B  C  D
    feature :         E  M

Both commits D and E are still here, but we create merge commit M that inherits changes from both D and E.

Merging is nice because it’s a non-destructive operation. The existing branches are not changed in any way. The feature branch will have an extraneous merge commit every time you need to incorporate upstream changes. If master is very active, this can pollute your feature branch’s history quite a bit. It can make it hard for other developers to understand the history of the project.

#### Rebase:
git checkout feature
git rebase master

    master  : A  B  C  D
    feature :            M

We create commit R, which actual file content is identical to that of merge commit M above. But, we get rid of commit E, like it never existed. Because of this obliteration, E should be local to developer Ed and should have never been pushed to any other repository.

The major benefit of rebasing is that you get a much cleaner project history. First, it eliminates the unnecessary merge commits required by git merge. Second, as you can see in the above diagram, rebasing also results in a perfectly linear project history. Re-writing project history can be potentially catastrophic for your collaboration workflow. And, less importantly, rebasing loses the context provided by a merge commit—you can’t see when upstream changes were incorporated into the feature.

#### The Golden Rule of Rebasing
The golden rule of git rebase is to never use it on public branches.

#### When to use
If the feature branch you are getting changes from is shared with other developers, rebasing is not recommended, because the rebasing process will create inconsistent repositories. For individuals, rebasing makes a lot of sense.

If you want to see the history completely same as it happened, you should use merge. Merge preserves history whereas rebase rewrites it.

## Workflows

 - **Centralized Workflow**
Centralized Workflow uses a central repository to serve as the single point-of-entry for all changes to the project. Instead of trunk, the default development branch is called master and all changes are committed into this branch. This workflow doesn’t require any other branches besides master.
The Centralized Workflow is great for small teams. The conflict resolution process detailed above can form a bottleneck as your team scales in size. This workflow doesn't get benefits of feature branch.

 - **Feature branching**
The core idea behind the Feature Branch Workflow is that all feature development should take place in a dedicated branch instead of the master branch. This encapsulation makes it easy for multiple developers to work on a particular feature without disturbing the main codebase. It also means the master branch will never contain broken code, which is a huge advantage for continuous integration environments.
**Features:**
Focused on branching patterns
can be leveraged by other repo oriented workflows
promotes collaboration with team members through pull requests and merge reviews
 
 - **Gitflow Workflow**
Gitflow is ideally suited for projects that have a scheduled release cycle. This workflow doesn’t add any new concepts or commands beyond what’s required for the Feature Branch Workflow. Instead, it assigns very specific roles to different branches and defines how and when they should interact. In addition to feature branches, it uses individual branches for preparing, maintaining, and recording releases.
The Gitflow Workflow defines a strict branching model designed around the project release. This provides a robust framework for managing larger projects.  
The git-flow toolset is an actual command line tool that has an installation process. 
**Develop and Master Branches**
Master: The master branch stores the official release history, and the develop branch serves as an integration branch for features. It's also convenient to tag all commits in the master branch with a version number.
Develop: Develop branch serves as as integration branch for features.  
**The overall flow of Gitflow is:**
    1. A develop branch is created from master
    2. A release branch is created from develop
    3. Feature branches are created from develop
    4. When a feature is complete it is merged into the develop branch
    5. When the release branch is done it is merged into develop and master
    6. If an issue in master is detected a hotfix branch is created from master
    7. Once the hotfix is complete it is merged to both develop and master

 
 - **Forking Workflow**
Instead of using a single server-side repository to act as the “central” codebase, it gives every developer their own server-side repository. This means that each contributor has not one, but two Git repositories: a private local one and a public server-side one. The Forking Workflow is most often seen in public open source projects.
 The main advantage of the Forking Workflow is that contributions can be integrated without the need for everybody to push to a single central repository. Developers push to their own server-side repositories, and only the project maintainer can push to the official repository. This allows the maintainer to accept commits from any developer without giving them write access to the official codebase.
The following is a step-by-step example of this workflow.

    1. A developer 'forks' an 'official' server-side repository. This creates their own server-side copy.
    2. The new server-side copy is cloned to their local system.
    3. A Git remote path for the 'official' repository is added to the local clone.
    4. A new local feature branch is created.
    5. The developer makes changes on the new branch.
    6. New commits are created for the changes.
    7. The branch gets pushed to the developer's own server-side copy.
    8. The developer opens a pull request from the new branch to the 'official' repository.
    9. The pull request gets approved for merge and is merged into the original server-side repository
