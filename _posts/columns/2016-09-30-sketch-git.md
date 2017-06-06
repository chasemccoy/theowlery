---
title: Sketch + Git
date: 2016-09-30 00:00:00 Z
---

If you do any sort of interface design in a team environment, you have probably run into the following scenario: you edit some mockups, export them, and then send them to your developers. Then you make some changes, and send them again. Next thing you know, you’ve got 24 copies of the mockups and each one is different and your developers don’t know which one is the latest and everything is chaos. 

Well, I had this problem at least. The company I work for doesn’t purchase copies of Sketch for everyone, so I couldn't just throw my Sketch document into a repo and share it with the developers. I found an even better solution. 

Mathieu Dutour has created [the amazing Git Sketch Plugin](https://mathieudutour.github.io/git-sketch-plugin/). This plugin adds some very useful features to Sketch that make working with a team of developers so much easier.

To get started, install the plugin and place your Sketch file in  the repo for your project. The workflow from there looks like this:

1. Make some changes in your Sketch file.
2. Use the plugin menu to commit your changes.
3. Use the plugin menu to push your changes. 

Whenever you commit, the plugin will ask for a commit message and then it will *automatically export the mockups that have been edited since the last commit*. This way, whenever you make changes and commit, the latest mockups (and only the latest mockups) will automatically be exported to the repo. Then, your developers can just pull and feel confident that they always have the latest mockups.

What’s extra cool is that you can even view diffs on the mockups, so that you can compare side by side the changes from past commits until the latest.

This plugin has made working on my team so much more efficient and easy for everyone involved. I can’t recommend it enough. 

[Download the plugin and make your life better](https://mathieudutour.github.io/git-sketch-plugin/).