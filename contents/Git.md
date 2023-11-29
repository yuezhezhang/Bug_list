## Git
1. Git submodule 
* [easy way to pull all submodules](https://stackoverflow.com/questions/1030169/easy-way-to-pull-latest-of-all-git-submodules)
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
