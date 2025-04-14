## Git
1. Git submodule 
* [easy way to pull all submodules](https://stackoverflow.com/questions/1030169/easy-way-to-pull-latest-of-all-git-submodules)
  * first time `git submodule update --init --recursive`
  * otherwise `git submodule update --recursive`
* [common code already exists in the index](https://stackoverflow.com/questions/12898278/issue-with-adding-common-code-as-git-submodule-already-exists-in-the-index)
* [some steps](https://www.jianshu.com/p/9000cd49822c)
* [git submodule push](https://stackoverflow.com/questions/5814319/git-submodule-push/10878273#10878273)
* [push submodule to remote](https://stackoverflow.com/questions/8372625/git-how-to-push-submodule-to-a-remote-repository)
* [how to push third party code to my repository](https://segmentfault.com/a/1190000009928515) **-- remaining issue**
2. [GnuTLS recv error (-110)](https://stackoverflow.com/questions/52529639/gnutls-recv-error-110-the-tls-connection-was-non-properly-terminated)
  * Recompile and install git
  * remove libcurl4-gnutls-dev, install libcurl4-openssl-dev
3. Clone someone else's repo and push to your own repo
  * See [here](https://stackoverflow.com/questions/18200248/cloning-a-repo-from-someone-elses-github-and-pushing-it-to-a-repo-on-my-github)
  * Create a new repository at github.com. (this is your repository)
    - Give it the same name as the other repository.
    - Don't initialize it with a README, .gitignore, or license
  * Clone the other repository to your local machine.
     ```
     git clone https://github.com/other-account/other-repository.git
     ```
  * Rename the local repository's current 'origin' to 'upstream'.
    ```
    git remote rename origin upstream
    ```
  * Give the local repository an 'origin' that points to your repository.
    ```
    git remote add origin https://github.com/your-account/your-repository.git
    ```
  * Push the local repository to your repository on github.
    ```
    git push origin main
    ```
 4. [**Guide for managing a ros project with Git**](https://robotics.stackexchange.com/questions/81431/guide-for-managing-a-ros-project-with-git)
  * git strategy for catkin and package folders (#q257855)
  * Best practice: one git repo per package? (#q218498)
  * What should I upload exactly to GitHub (#q173960)
  * Using git for version control with catkin and Eclipse (#q216664)
 5. [Make the current branch a master branch](https://stackoverflow.com/questions/2763006/make-the-current-git-branch-a-master-branch), [tutorial](https://www.w3docs.com/snippets/git/how-to-make-the-current-git-branch-a-master-branch.html)
    ```
    git checkout better_branch
    git merge --strategy=ours master    # keep the content of this branch, but record a merge
    git checkout master
    git merge better_branch             # fast-forward master up to the merge
    ```
 6. [Compare between branches](https://www.git-tower.com/learn/git/faq/git-compare-two-branches)
  * Compare actual changes
    ```
    git diff main..another_branch
    ```
  * Compare commits
    ```
    git log main..another_branch
    ```
  * Compare a specific file
    ```
    git diff main..another_branch file
    ```
 7. Failed to connect to github.com port 443: Operation timed out
  * In Linux, see [here](https://www.jianshu.com/p/471aeba64724). In Windows, see [here](https://developer.aliyun.com/article/1077240)
  * Search the IP address of github.com and github.global.ssl.fastly.net in [https://sites.ipaddress.com/](https://sites.ipaddress.com/)
  * Copy paste in the hosts files
    ```
    sudo vi /etc/hosts

    --------------------
    140.82.112.3    github.com
    151.101.1.194   github.global.ssl.fastly.net
    --------------------
    ```
  8. [How to add license](https://gist.github.com/nicolasdao/a7adda51f2f185e8d2700e1573d8a633)
  9. [Impossible to center a table in GitHub readme](https://stackoverflow.com/questions/44172954/is-it-possible-to-have-a-table-in-the-center-in-a-github-gist-markdown)
  10. [GitHub markdown notes](https://gist.github.com/nikhilnayyar002/7a35e653d3d590e317c829243e73b110)
  11. [Revert committed changes](https://stackoverflow.com/questions/10780228/how-can-i-revert-multiple-git-commits-already-pushed-to-a-published-repository)
      ```
      // a specic commit
      git revert _commit_id
      # Revert a series using commit hashes.
      git revert --no-edit <last_good_commit>..<last_bad_commit>
      ```
