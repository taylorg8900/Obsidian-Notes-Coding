
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