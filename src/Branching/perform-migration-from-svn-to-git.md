---
title: Perform the migration from SVN to Git
description: Explore the feature isolation branching strategy and explore when and how to delete branches
ms.assetid: 
ms.prod: 
ms.technology: 
ms.manager: 
ms.date: 
ms.author: hkamel
author: hkamel
---

# Perform the migration from SVN to Git


## Requirements


## Understand git-svn
in this article we will rely on git-svn command to perform the migrations. [git svn](https://git-scm.com/docs/git-svn) is a simple conduit for changesets between Subversion and Git. It provides a bidirectional flow of changes between a Subversion and a Git repository.

### Limitations
#### Author Information
SVN and Git are difefrent when it comes to how it store the author infromation. 

#### Tags

## Steps to migrate

# Migrate from SVN to Git
SVN migrations to Git can vary in complexity, depending on how old the repository is and how many branches were created and merged, as well as if you use regular SVN or close relative like SVK to do the branching and merging. If you have a fairly new repository and the standard setup of a trunk, branches, and tags directory, the migration process could be straighfoward. However if your team has done a lot of branching and merging, or your repository follows a non-standard directory setup, or that setup changed over time, the migration process could be considerably more complex. 

There are several ways to migrate from SVN to Git. This approach is based on using [git-svn](https://git-scm.com/docs/git-svn), a Git extentsion which can be used to checkout a Subversion repository to a local Git repo and then push changes from the local Git repo back to the Subversion repository. These steps provide a detailed overview of the process for migrating from SVN to Git in a Windows envrionment, without syncronization back to the original SVN repository. The end result will be a bare Git repository for sharing with the rest of your team.

Before you try to migrate your source code from a centralized version control system to Git, be sure that you familiarize yourself with the differences between centralized and distributed version control systems, and plan your team’s migration. After you’ve prepared, you can begin the migration.

The high level workflow for migrating from SVN-to-Git is as follows:
* Prepare migration envrionment
* Convert the source SVN repository to a local Git repository
* (Optional) - Synchronize the local Git repository with any changes from SVN repository while developers continue using SVN
* Push the local Git repository to a remote Git repository hosted on Visual Studio Team Services
* Lock SVN repository, synchronize any remaining changes from SVN repository to local Git repository and push final changes to VSTS remote Git repository
* Developers begin using Git as main source control system

## Prepare Migration Environment
A migration environment should be configuired on a local workstation. The following applications or utilities will need to be installed on the migration workstation:
* [Git](https://git-scm.com/downloads)
* [Subversion](http://subversion.apache.org/packages.html)
* [git-svn utility](https://www.kernel.org/pub/software/scm/git/docs/git-svn.html)

You will also need to create a Git repository on your VSTS account to host the converted SVN repository.

## Convert the source SVN repository to a local Git repository
The goal of this step is to convert the source Subversion repository to a local *bare* Git repository. A *bare* Git repository does not have a local working checkout of files that can be modified. This is the recommended format for sharing a Git repository via a remote repository hosted on a service like VSTS.

### Retrieve a list of all Subversion authors
Subversion just uses the username for each commit. Git stores more data for each author but at a minmal, each commit will need a name and an email. The git-svn tool will list the SVN username in the author and email fields. However, you can create a list of all SVN users along with their corresponding Git names and emails. You can then use this list in the git-svn tool to transfrom SVN users into well formatted Git authors. 

From the root of your local Subversion checkout, run this command:

```
svn log -q | awk -F '|' '/^r/ {sub("^ ", "", $2); sub(" $", "", $2); print $2" = "$2" <"$2">"}' | sort -u > authors-transform.txt
```
This command will retrieve all the log messages, extract the usernames, eliminate any duplicate usernames, sort the usernames and place them into a “authors-transform.txt” file. You can then edit each line in the file to create a mapping of SVN users to a well formatted Git user. For example, you can map `jdoe = jdoe <jdoe> ` to `jdoe =  John Doe <john.doe@email.com>` .

### Clone the Subversion repository using git-svn
The following command will do the standard git-svn transformation using the authors-transform.txt file created in the previous step. It will place the Git repository in the "c:\mytempdir" folder in your local machine. 
```
git svn clone ["SVN repo URL"] --prefix=svn/ --no-metadata --authors-file "authors-transform.txt" --stdlayout c:\mytempdir
```
The –prefix=svn/ is necessary because otherwise the tools can’t tell apart SVN revisions from imported ones. Setting a prefix (with a trailing slash) is strongly encouraged in any case, as your SVN-tracking refs will then be located at "refs/remotes/$prefix/", which is compatible with Git’s own remote-tracking ref layout (refs/remotes/$remote/). Setting a prefix is also useful if you wish to track multiple projects that share a common repository. By default, the prefix is set to origin/.

If you are using the standard trunk, branches, tags layout you’ll just put –stdlayout. However if you have something different you may have to pass the –trunk, –branches, and –tags in to identify what is what. For example if your repository structure was trunk/companydir and you branched that instead of trunk, you would probably want ‘–trunk=trunk/companydir –branches=branches‘. 

This command can take a few minutes to several hours depending on the size of the SVN repository. Upon completion, you will have a Git checkout of your repository. 

### Convert svn:ignore properties to .gitignore
If your svn repo was using svn:ignore properties, you can  convert this to a .gitignore file using:
```
cd c:\mytempdir
git svn show-ignore > .gitignore
git add .gitignore
git commit -m 'Convert svn:ignore properties to .gitignore.'
```

### Push repository to a bare git repository
In this step, you will create a bare repository and make its default branch match SVN's trunk branch name.

1. Create a bare Git repository.
```
git init --bare c:\new-bare.git
cd c:\new-bare.git
git symbolic-ref HEAD refs/heads/trunk
```
2. Push the local Git repository to the new bare Git repository
```
cd c:\mytempdir
git remote add bare c:\new-bare.git
git config remote.bare.push 'refs/remotes/*:refs/heads/*'
git push bare
```
3. Rename "trunk" branch to "master"
Your main development branch will be named “trunk” which matches the name it was in Subversion. You’ll want to rename it to Git’s standard “master” branch using:
```
cd c:\new-bare.git
git branch -m trunk master
```
4. Clean up branches and tags
git-svn makes all of Subversions tags into very-short branches in Git of the form “tags/name”. You’ll want to convert all those branches into actual Git tags or delete them.

Migrate SVN tags to be Git tags
```
cd c:\new-bare.git
git for-each-ref refs/remotes/tags | cut -d / -f 4- | grep -v @ | while read tagname; do git tag "$tagname" "tags/$tagname"; git branch -r -d "tags/$tagname"; done  

```

Create all the SVN branches as proper Git branches
```
git for-each-ref refs/remotes | cut -d / -f 3- | grep -v @ | while read branchname; do git branch "$branchname" "refs/remotes/$branchname"; git branch -r -d "$branchname"; done  

```




## Reference information
- [Branching Strategies with TFVC (new guidance)](./branching-strategies-with-tfvc.md)
- [Branching and Merging Guidance (latest copy of classic guidance)](https://vsardata.blob.core.windows.net/projects/TFS%20Version%20Control%20Part%201%20-%20Branching%20Strategies.pdf)
- [Continuous Integration](https://www.visualstudio.com/learn/what-is-continuous-integration/)
- [Feature Toggles](https://msdn.microsoft.com/en-ca/magazine/dn683796.aspx)
- [Team Foundation Version Control (TFVC)](https://www.visualstudio.com/en-us/docs/tfvc/overview)

> Authors: Hosam Kamel, William H. Salazar
 
*(c) 2017 Microsoft Corporation. All rights reserved. This document is
provided "as-is." Information and views expressed in this document,
including URL and other Internet Web site references, may change without
notice. You bear the risk of using it.*

*This document does not provide you with any legal rights to any
intellectual property in any Microsoft product. You may copy and use
this document for your internal, reference purposes.*