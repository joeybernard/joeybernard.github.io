.. title: Using git for your config
.. slug: using-git-for-your-config
.. date: 2020-03-19 23:14:38 UTC-03:00
.. tags: git admin
.. category: howto 
.. link: 
.. description: 
.. type: text

Now that my new blog is starting to come together, I need to start moving content over. The first item is the most
important whenever I setup a new Linux system. Some time ago, I moved all of my user level configuration over to a github
repository. You can configure a system with the following code::

   mkdir .myconfig
   echo .myconfig >>.gitignore
   git clone --bare https://github.com/username/myconfig.git $HOME/.myconfig
   alias config='/usr/bin/git --git-dir=$HOME/.myconfig --work-tree=$HOME'
   config checkout

You may have some files that already exist in your home directory that you will need to either delete or move aside to
finish the checkout. It is also helpful to add the config alias to your .bashrc or .profile file so that you have it 
always ready. You need to always use these command line options to git, so you might as well have this alias set to make
your life easier. Hopefully you find it useful.
