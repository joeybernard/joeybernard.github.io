.. title: O Problems in bash
.. slug: o-problems-in-bash
.. date: 2021-03-14 21:37:57 UTC-03:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text

Recently, I ended up with a bit of a weird problem at work. We collect data files that need to be processed every 15 minutes. At the hour mark, we need to process files that have been collecting data over the last 15 minutes of the previous hour. The way I originally wrote the script, it would use the date command to get the current hour and then use bash arithmetic to subtract one from it. But, I was seeing weird behaviour around 0800 hours. What the heck was going on here?

What I didn't realize was that bash uses a zero at the beginning of a number to identify it as an octal number. So what do you think happens when you get a two-digit number as a string from an external program, like date? At 0800 hours, you get an error because 08 is not a valid octal number. Of course, you don't get an error message that actually makes sense given this problem. So it took some creative Googling to actually figure out what assumption had bitten me in the back-side.

Luckily, the date command allows you to get things like the current hour value, minus X number of hours. This was a much cleaner, better way to handle this type of arithmetic. Hopefully, this is of some use to other people running into their own blind spots.
