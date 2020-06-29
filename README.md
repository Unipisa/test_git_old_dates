# test_git_old_dates

Repostiory to test a git branch with full support for pre 1970 dates
[https://github.com/git/git/compare/master...peff:jk/time-negative](https://github.com/git/git/compare/master...peff:jk/time-negative)

To get te modified version of git

```bash
git clone https://github.com/peff/git.git
cd git
git checkout jk/time-negative
make
```

you will get

```
./git --version
git version 2.21.0.rc0.5167.g75a411b713
```

Then, to test pre 1970 dates

```bash
cd test_git_old_dates
../git/git init
touch test_now.txt
../git/git add .
../git/git commit -m "now"
touch test_past.txt
../git/git add .
../git/git commit -m 'Great Scott!' --date="Mon, 5 Nov 1956 12:00:00 EST"
```

and we can visualize with `gitk` 
and with `../git/git log`
```
commit 5cd7764bbc9e75f76c70bc24a8a44d095c7d6e9d (HEAD -> master, origin/master)
Author: Guido <guido.scatena@unipi.it>
Date:   Mon Nov 5 12:00:00 1956 -0500

    Great Scott!

commit eb5268250a7bc2cc95d8df8c44ee4a5c0b3326af
Author: Guido <guido.scatena@unipi.it>
Date:   Tue Jun 30 00:10:21 2020 +0200

    now
```

(please note that standard git log gives wrong dates)
```
Thu Jan 1 00:00:00 1970 +0000
```

In order to push to GitHub the repository must have
disabled the fsck check for badDateOverflow
(for the moment only GitHub Support can do this).

Otherwise we get
```
remote: error: object 5cd7764bbc9e75f76c70bc24a8a44d095c7d6e9d: badDateOverflow: invalid author/committer line - date causes integer overflow
```



´´
