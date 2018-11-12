---
title: Several submit actions in one form
date: 2018-10-22 22:18:58
tags:
- eng
- html
---

Sometimes you need to have several actions to be submitted on the same form. Usually you only have one button for this which points to the place you define on the `FORM ACTION` block.
So, how can you detect which button was clicked in plain HTML?

You can use the `value` variable on button, this way:

```
<FORM METHOD="whatever" ACTION="/your/endPoint/">


<button name="btnaction" value="accept" class="..." type="submit">Accept 1</button>"
<button name="btnaction" value="dontAccept" class="..." type="submit">Dont Accept</button>"
<button name="btnaction" value="maybe" class="..." type="submit">Maybe Accept</button>"
```

And in your code just check the `btnAction` parameter variable for `accept`, `dontAccept` or `maybe` values.  Easy!


