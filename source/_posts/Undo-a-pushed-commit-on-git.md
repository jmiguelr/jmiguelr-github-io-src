---
title: Undo a pushed commit on git
date: 2018-11-28 11:08:49
tags:
- eng
- git
---

We all know it. Shit happens.

Today, I screw a small piece of code ( thank you SonarLint! ;-) (*)).  It was just a small optimization, but after checking with a coworker the code we couldn't find what was going wrong but the reality was that something was broken so I decided to go back in time.

The commits (2 commits) was already pushed to our bitbucket and tried several approaches. I created a detached branch, modify and commit. No success. Then I tried some of features IntelliJ gaves me, but I could find a good one.

So finally I found ([stackoverflow at rescue](https://stackoverflow.com/questions/4114095/how-to-revert-a-git-repository-to-a-previous-commit)) this solution which help **in my case**.  Be careful: my problem may be different than yours and so the solution. Even more, the solution I used it's not the choosen as the best on previous link.

I had the following git history


```
commit 2071cf3cb8
Author: xxxxx
Date:   Wed Nov 28 10:16:48 2018 +0100

commit 5ff2c4a3a1
Author: xxxxx
Date:   Wed Nov 28 10:11:06 2018 +0100

commit 3a37cbc8e7
Author: yyyyy
Date:   Wed Nov 28 09:58:33 2018 +0100
```

The two top commits was mine, and was wrong. I wanted to go back to 3a37cbc8e7 so I use the following sequence:

```
# Resets index to former commit; replace '3a37cbc8e7' with your commit code
git reset 3a37cbc8e7

# Moves pointer back to previous HEAD
git reset --soft HEAD@{1}

git commit -m "Revert commit to the past"

# Updates working copy to reflect the new commit
git reset --hard
```

Here is the point where you're back to the commit you wanted to be. Check it. If you're satisfied, just push it.

And additional benefit with this approach is that you don't loose your history: there will be ever a culprit (myself, in this case) written on the chain.

Hope this helps.


(*) PS: Of course, the blame on SonarLint it's just a joke. The fault was mine :-)
