.. title: Bad Information from a Long Time Ago
.. slug: bad-information-from-a-long-time-ago
.. date: 2021-10-08 10:11:53 UTC-03:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text

I am a firm believer in the idea that we should always be learning and always be willing to change our ideas based on new information. This includes being willing to admit that we had something wrong for a long time and be able to step outside yourself and realize that you need to let things go. I had this happen to me this past week. We were playing around with file permissions for temporary files, and I realized that I had gaps in my knowledge. The first big one was that I had not realized that there were 4 groups of permissions for files, not just 3. I had completely missed the fact that setuid, setgid and the sticky bit actually formed a fourth permission group that could be set with chmod. I also realized that some early misinformation had conflated setuid, setgid and the sticky bit in my head. Because of this, I simply didn't realize that the sticky bit wasn't simply a synonym for either setuid or setgid. Even after using Linux for nearly 30 years, I still have these little pockets of early misunderstood items that just never got corrected. With any luck, I'll be able to keep fixing these little mental hiccups for a long, long time.
