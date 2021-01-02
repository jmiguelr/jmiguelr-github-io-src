---
title: My new 2FA setup - Authy + oathtool
date: 2021-01-02 11:23:58
tags:
- eng
- linux 
 
---

So long!.  I know, 2020 has been such a strange year. For me, it also was the first time (yes, in my life) I switched to another company. Coming from being self-employed on my own company, it was a great challenge but I'm really happy about it. Even I had to be forced to keep my mind fully in focus for work. 

Anyway: I want to talk about my new security setup for internet applications. I had some spare time and a huge To-Do list but this was one of my top priorities. I've been using 2-factor authentication (2FA) for some time with the [Google Authenticator](https://play.google.com/store/apps/details?id=com.google.android.apps.authenticator2&hl=es&gl=US) android application.  But I was not fully satisfied with it. 

Sometimes I want to authenticate on desktop applications and I'd like to be able to do it from my computer. But I'd also like to be in sync with the phone application. Or just be free to know the seed for any service I use to feel it as *mine* (I could reuse the bitcoin *motto* "not your keys, not your coins" here).

Also, I was using the [HyperFido keys I wrote about](https://jmiguelr.github.io/2020/01/19/Getting-Hyperfido-U2F-keys-working-on-Linux-Ubuntu-or-Mint/) in just two places, so I wanted to extend the use. 

So: first move was to find a replacement for the mobile app with enough freedom and I choose [Authy](https://authy.com/). It also has some cloud sync utilities I don't plan to use. I just want to keep my seeds for the sites I use (and also a good improvement: password protected beyond the mobile protection). 

Second: find a way to get the 2FA tokens (One-Time Passwords, OTP) on Linux. As easy as `sudo apt install oathtool` . With this small tool you can get your One-Time Passwords easily. 

So, the final step was going for every important service I use and change the security setup. Some of them (Firefox, Dropbox) forces you to remove all 2FA previous setup before starts with a new one. Others (Google) will let you change only what you need (so you don't need to re-register your Fido keys if you just want to change your OTP setup).

In all the cases the procedure is very similar: the site you register will allow you both scans a QR-code or manually enter a chain of letters (usually 6 groups of 4 letters each, sometimes more or fewer letters).  This is your seed for that site. Keep it safe and secret (my choice is to save it on keepass, together with the real password for that site).  

Now you can use that string on Authy to add your site on your mobile device. Even while Authy has that option, I prefer not to upload my seeds to their cloud, but it's up to you. I understand it's a good way to have the codes in sync for several devices, or just for having a backup of the seeds, but I don't need it (and I don't like it)

And of course, the last piece for having generated OTP on Linux is `oathtool` on command line. Just type 

```
oathtool --base32 --totp abcdefghijklmnopqrstuvwxyz
``` 

(obviously, with your real seed code) to get the OTP you need to login. 

Is this a perfect solution?. For sure, It isn't. I'm not fully satisfied having in the same place both the password for the site and the 2AF seed. I could have two keepass different files but I don't feel it as a need right now. 

Also: I'm using this OTP system as a backup for the preferred 2FA way: the physical Fido keys. After almost one year of using them I can conclude they are a very good way to get authenticated. I own 2 Fido keys so I can have one of them always with me and the other on a safe place as backup. Not every site allows to have several keys (cannot understand why, I hope it will eventually fix it)

Well, that's all!.  I hope this system for keeping your accounts more secure helps you.  As long as right now there's no comments system available for this site, tell me whatever you think about this setup via Twitter: [@jmiguel](https://twitter.com/jmiguel)


