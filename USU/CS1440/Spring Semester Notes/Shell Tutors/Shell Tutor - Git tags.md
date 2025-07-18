
# lesson 1

commit be3268e58e3a39588436fbb5531f18f392023d0e (HEAD -> master, tag: final, origin/master, origin/HEAD)
- `commit be3268e` is the SHA-1 fingerprint of this commit
- `HEAD -> master`
	- the commit HEAD is the tip of a branch named master
- `tag: final` means the commit is tagged with the name final
- `origin/master, origin/HEAD` 
	- 'indicates this commit is also the tip of the master branch on the remote server, and that this commit is what's currently checked-out there'
	- doesn't make sense right now but probably will later

git push -u origin master
- -u flag tells git that `origin` is the default desitination when you run `git push`
- if we don't do this we need to type out `git push origin master` each time we want to push which is annoying

pushing tags to a remote 
- git does not automatically push tags because they are commonly used on the local computer only, if you want tos hare them you have to be explicit
- `git push origin TAG_NAME`
- `git push origin --tags` or `git push --tags` to push every tag at the same time

git tag
- run `git help tag` to find out what you can do with `git tag`
	- for example: `git tag -l` shows all of the tags in the repo currently
- creating a tag looks like `git tag TAGNAME [commit]`
	- `[commit]` is optional, but if you use it it is an ID such as be3268e or whatever. if you don't include it the tag gets placed on the currentlly checked out commit (HEAD)
- no limits on amount of tags a commit can have

moving tags
- done in two steps: delete it, then re make it on a new commit
- `git tag -d TAGNAME` to delete a tag
- `git push -d <remote> <tag>` to delete the tag from the remote (need to do this as well)
- `git tag TAGNAME [commit]` to re create it
- make sure to also push the commit to gitlab or github after, pushing the tag wont also push the commit

# lesson 2 - using git tags in a project
will learn:
- add development phase tags to commits in a project
- push tags to your remote repo

tags we will use on projects to mark commits
- `analyzed` marks the end of the requirements analysis phase
- `designed` marks the end of the design phase
- `implemented` makrs the end of the implementation phase
- `tested` marks the end of the testing phase
- `deployed` marks the end of the deployment phase

git log --stat
- shows the files that were changed along with how much each file ws changed


