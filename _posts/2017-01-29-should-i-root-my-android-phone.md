---
published: true
title: Should I root my Android Phone?
layout: post
---
Android is an operating system developed by Google, primarily for Mobile Phones. Android is based on the Linux kernel and inherits it's permissions structure. The operating system itself runs as the SuperUser or root and allows the user of the phone to perform tasks as a non-privileged one.

## Why do you have to root

The reason Android doesn't give root permissions to the user by default is because the power of root is limitless. Once an application is granted root access it could potentially read all of your saved passwords, credit cards and other sensitive information from any app in your mobile phone and could even compromise your Wifi passwords.

Furthermore it could do permanent damage to your operating system that you couldn't fix without a reinstall, resulting in data loss for you. Your OEMs are actually being responsible when they patch the vulnerabilities in your phone that allow you to get root access.

You could only fix your compromised mobile phone by reinstalling it's operating system and it's not something everybody can do. Even if you can do it, doesn't mean you won't accidentally brick your phone.

While rooting your phone will give you full power to your operating system, it will also void your warranty in most of the countries and will block you out from services like Android Pay, Samsung Pay and similar services.

## But I still want to root my phone

If you have really made up your mind, then be careful in how you distribute root permissions to applications. There are two main concerns about usage of root permissions

0. Which su binary you use
0. Which applications you grant root access to

If you are confused about the first one, remember that [SuperSU was bought by a chinese company][1] and one user even went as far to say [it was sending out weird internet traffic][1]. Remember, this is all of your privacy you are trusting your root management application with. Your root management application (that interacts directly with su binary) has full root access and manages prompts of other applications requesting root access so choose the one you trust the most. I personally find Phh superuser to be trust worthy.

Remember, there is no undo button with root. Once you give the wrong application root access it'll infect your phone quicker than you realize maybe without you even noticing it's happened. So be paranoid about giving applications root access.

## How about a custom firmware from XDA

Again, custom firmwares on XDA are modified in ways you might not even know. You don't know for sure that the Firmware you installed doesn't have spyware on it and won't send all of your passwords to some hacker's servers. Your best bet if you value your privacy is sticking with unrooted Stock Firmware.

## Closing thoughts

I am writing this all out because I voided my warranty and my sense of security thinking I'll get better customizability with a rooted Custom Firmware. It wasn't worth it, I couldn't get my Gear VR working on Lineage OS because it's Samsung only. and the latest LineageOS doesn't even have a Theme Editor so my root wasn't even worth the trouble. I knew what I was in for but I wasn't. I ended up restoring to stock with my knox counter tripped. Don't do what I did people.

[1]:http://www.androidpolice.com/2015/09/29/chainfire-transfers-ownership-of-supersu-to-ccmt-will-remain-involved-in-the-project-for-two-more-years/
[2]:https://www.reddit.com/r/AndroidQuestions/comments/55io5z/best_open_source_alternative_to_supersu/d8bgzvt/
