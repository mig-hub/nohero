NoHero
======

NoHero is an excuse to make a tutorial about scripting. But it is also a functional tool which let's you initialize and control a web application in a way similar to how you would do with [Heroku](https://www.heroku.com).

How to install
--------------

The most practical way is to clone the repository in your desired location:

```bash
cd ~/forks
git clone https://github.com/mig-hub/nohero.git
```

And then create a symlink to a location that is in your $PATH. I personally use "~/bin":

```bash
ln -s ~/forks/nohero/nohero ~/bin/nohero
```

It should be executable already, but if it isn't, then:

```bash
chmod +x ~/bin/nohero
```

Considerations
--------------

Here is a list of implementation details that you may want to consider if you're going to use this script. They may change in the future because I will continue improving it. And also you are encouraged to use this script as a base to create your own custom one.

All scripts are written in [Bash](https://en.wikipedia.org/wiki/Bash_%28Unix_shell%29) since it is installed on most unix-based distributions (GNU/Linux, OSX, etc) for both local machines and remote servers.

While the script may work on other remote servers, it is tested on **Ubuntu 18.04.3 (LTS) x64**. This implies that it is a GNU/Linux operating system using `apt` as a package manager. It also uses the recommended command `apt` as opposed to `apt-get` which I believe was available since 2016.

I usually get my servers on [Digital Ocean](https://m.do.co/c/a78c8d2aa8f1) and if you click the following link, you can [get 100$ in credit](https://m.do.co/c/a78c8d2aa8f1). 

Regarding the credential method, **NoHero** assumes that you have root access using an SSH key. Having a password will not be a problem, but the script will fail if `root` does not have a "/root/.ssh" directory because it will create a new user called `nohero` who can only login via an authorized SSH key, not a password. During `server:init`, it will copy the ".ssh" directory from `root`. That is why `root` needs SSH key access. If you further want to change the keys, there are other sub-commands to do so. This all may change in the future depending on what is the best balance between security and practicality.

Since we create a user without password access, we need a way to give access to `sudo` commands. The solution we use so far is that we edit the "/etc/sudoers" file and add the following line to it if there is no line starting with "nohero ".

```
nohero ALL=(ALL) NOPASSWD:ALL
```

Again, this may change in future versions depending on what is the best solution. After `server:init` feel free to use `visudo` and change this to something more appropriate. Or even better, submit a pull request if you feel you have a better solution.

Most sub-commands, including `server:init` are written with checks in such a way that you can run them multiple times and not create an issue. For example `server:init` will just tell you if the user `nohero` already exist, or if a package is already installed. It will ask for confirmation before any connection and ask you if you want to upgrade a package when it is already installed.

Like Heroku, the NoHero assumes that you deploy your changes with [Git](https://git-scm.com/) and uses git hooks on the server to accomplish tasks like checking out and restarting the server. NoHero will complain if you don't have Git installed.

Regarding the license of this software, please have a look at the "LICENSE" file.

Commands
--------

**This section will be written when we have a better understanding of what the final API will be.**

