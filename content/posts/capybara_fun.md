+++
title = 'Capybara Fun'
date = 2026-07-10
draft = false
tags = ['ruby', 'rails', 'capybara', 'testing', 'debugging']
+++

I just *love* Ruby on Rails. All of the automagic that happens makes trying to test or debug *so* simple. In case it isn't clear, there is just a tad of sarcasm there.

I had what I thought was some very minor changes on a page. We had some panes on a page, and you navigated between them by clicking on tabs that had an icon and a label. We were running out of screen real estate, so we decided to remove the icons. We were using tailwind, and had some Javascript that would change the styling of the label and icon if the tab was selected. All pretty basic stuff.

So, I removed the icon and ran the tests. What do you know, capybara started having a bit of an issue. Not a worry, though, right? That's why we have tests. So that we can see exactly what the problem is. And so, rspec told me that it was seeing a submit button that should have gone away after the form gets submitted. So, I pull up the page in Chrome, check the rendered DOM, and followed the steps the test is doing and don't see any issues. What the heck?

Thinking about it for a while, I realized that the actual problem must be that capybara is not actually clicking the submit button in the first place. It just never told me that it had a problem with that. Now I had to try and figure out why it was having an issue finding and clicking the submit button. According to the DOM, it seemed like everything was cool. What was happening?

Remember when I mentioned that there was some Javascript earlier? That Javascript was supposed to change the styling of the icon that I just removed and was now failing quietly. That should be fine, as it doesn't affect any of the functionality or the rendering. Nope, not according to capybara. When that Javascript fails, capybara gives up on anything else and never clicks the submit button for the form. Which is fine, but why didn't it tell me that this was where the error happened. Not several steps later when it checked to see if the submit button successfully went away after the form was done. Argh!

I'm getting more of the weirdness of Ruby on Rails and capybara into my head. Hopefully it doesn't get too soft from beating it against a brick wall.
