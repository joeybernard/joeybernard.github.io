.. title: Github Satellite 2020
.. slug: github-satellite-2020
.. date: 2020-05-06 21:05:40 UTC-03:00
.. tags: devtools
.. category: News
.. link: 
.. description: 
.. type: text

I have been listening in to the talks being given as part of Github Satellite 2020. They have all been really good. I have been a git user for years, and a lot of this has been on Github. But I really had no idea how much I had been missing. Part of this lack in my own knowledge was due to the fact that I have been working on either solo projects or projects of 2-3 people. Now that I am starting to work in larger groups, I am realizing the power of things like pull requests. This is probably old hat to people who have been working with Github in larger organizations, but it is eye opening to us solo workers. I will definitely be following up further with my new group so that we can actually use all of the tools available.

I also have not had time to look into the new official cli utility to work with Github. It looks awesome. I have work in several remote servers where cli tools is really the only sane way to work. It looks like it will make my work there a lot easier. It doesn't look like it is in the package repositories for most Linux Distributions yet, so you will need to grab it directly from the releases page (https://github.com/cli/cli/releases). I also need to use the command line in Windows, at least occasionally. When I do, I use scoop to manage my development environment. Luckily, you can add a new bucket and install the Github cli with the following commands ::

    scoop bucket add github-gh https://github.com/cli/cli/scoop-gh.git
    scoop install gh

They also talked about new capabilities available in the official Github extension for VSCode. It will allow you to interact much more seemlessly with issues, code and PR's. It is looking more and more that I will be using VSCode as my day to day development tool. With the ability to connect remotely across to other machines, it is definitely pulling me away from Emacs. The only issue is that my work is divided between work locally and work SSH'ed into a remote machine. Because of this, I am still leaning towards an environment around vim, gh, bash and other cli tools. I guess I'll just have to wait and see how my day-to-day work shifts over the next few months.

