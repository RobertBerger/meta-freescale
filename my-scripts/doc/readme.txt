1) create a new repo on github

2) add my-scripts dir

cd meta-freescale

echo "# meta-freescale fork" >> README.md

git init

git add .

git commit -m "first commit"

git remote add origin git@github.com:RobertBerger/meta-freescale.git

git push -u origin master

3) use my repo

mv meta-freescale meta-freescale.ori
git clone git@github.com:RobertBerger/meta-freescale.git

4) add upstream

cd meta-freescale

git remote add official-upstream git://github.com/Freescale/meta-freescale

$ git fetch official-upstream

warning: no common commits
remote: Enumerating objects: 72, done.
remote: Counting objects: 100% (72/72), done.
remote: Compressing objects: 100% (44/44), done.
remote: Total 33435 (delta 34), reused 47 (delta 28), pack-reused 33363
Receiving objects: 100% (33435/33435), 42.65 MiB | 9.37 MiB/s, done.
Resolving deltas: 100% (18856/18856), done.
From git://github.com/Freescale/meta-freescale
 * [new branch]        dunfell     -> official-upstream/dunfell
 * [new branch]        master      -> official-upstream/master
 * [new branch]        master-next -> official-upstream/master-next
 * [new branch]        morty       -> official-upstream/morty
 * [new branch]        pyro        -> official-upstream/pyro
 * [new branch]        rocko       -> official-upstream/rocko
 * [new branch]        sumo        -> official-upstream/sumo
 * [new branch]        thud        -> official-upstream/thud
 * [new branch]        warrior     -> official-upstream/warrior
 * [new branch]        zeus        -> official-upstream/zeus
 * [new tag]           2.1         -> 2.1
 * [new tag]           2.2         -> 2.2


$ git branch -a

* master
  remotes/official-upstream/dunfell
  remotes/official-upstream/master
  remotes/official-upstream/master-next
  remotes/official-upstream/morty
  remotes/official-upstream/pyro
  remotes/official-upstream/rocko
  remotes/official-upstream/sumo
  remotes/official-upstream/thud
  remotes/official-upstream/warrior
  remotes/official-upstream/zeus
  remotes/origin/HEAD -> origin/master
  remotes/origin/master


5) use specific upstream branch/commit and make own branch

syntax: git fetch url-to-repo branchname:refs/remotes/origin/branchname

$ git fetch git://github.com/Freescale/meta-freescale dunfell:refs/remotes/origin/dunfell

From git://github.com/Freescale/meta-freescale
 * [new branch]        dunfell    -> origin/dunfell

6) Update from upstream:
git co master
>> git remote -v

official-upstream       git://github.com/Freescale/meta-freescale (fetch)
official-upstream       git://github.com/Freescale/meta-freescale (push)
origin  git@github.com:RobertBerger/meta-freescale.git (fetch)
origin  git@github.com:RobertBerger/meta-freescale.git (push)

>> git fetch official-upstream
remote: Counting objects: 4043, done.
remote: Compressing objects: 100% (1273/1273), done.
remote: Total 4043 (delta 3130), reused 3632 (delta 2727)
Receiving objects: 100% (4043/4043), 721.50 KiB | 402.00 KiB/s, done.
Resolving deltas: 100% (3130/3130), completed with 502 local objects.
From git://git://github.com/Freescale/meta-freescale
   62591d9..e758547  master     -> official-upstream/master
 + 2942327...a382678 master-next -> official-upstream/master-next  (forced update)
   a3fa5ce..6a1f33c  morty      -> official-upstream/morty
---

7) My own branch:
git co master
git co official-upstream/dunfell
git checkout -b 2020-08-28-dunfell
git co master
cd my-scripts
./push-all-to-github.sh

8) apply patches

cd meta-virtualization

git co 2019-09-09-warrior-2.7+

stg init

stg series

stg import --mail ../meta-virtualization-patches/2019-09-09-warrior-2.7+/0001-use-systemd-as-cgroup-manager-for-docker-While-it-s-.patch

import all patches

...

stg series

stg commit --all

git log

git co master

9) push to my upstream

my-scripts/push-all-to-github.sh

