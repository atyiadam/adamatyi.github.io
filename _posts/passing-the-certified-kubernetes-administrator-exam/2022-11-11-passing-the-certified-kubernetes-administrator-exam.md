---
title: Passing the Certified Kubernetes Administrator exam
date: 2022-11-11 10:29:00 +01:00
description: I recently passed the Certified Kubernetes Administrator program created by the Cloud Native Computing Foundation (CNCF), in collaboration with The Linux Foundation. This is what I did to clear the exam on my first attempt.
categories: kubernetes
tag:
- kubernetes
- cka
- cncf
---

## What is the CKA?

Earlier this year, our organization got gifted a couple of vouchers for the Certified Kubernetes Administrator program (CKA). This made me super excited, since each enrollment costs $395. CKA is considered to be the de facto standard when it comes to Kubernetes certifications. In case you are not familiar with [Kubernetes](https://kubernetes.io/) (k8s), it is a container orchestration platform, which – without all the fancy words – essentially is a place that makes running and maintaining applications for developers a lot easier. If you are planning to learn and understand how Kubernetes works and functions under the hood, the CKA is a great place to start. The program and the exam do not cover advanced features, but it contains a lot of hands on practice, which creates a great foundation for your k8s knowledge. After clearing the exam, you will have a proper tool belt to dive deep into the more exciting and also complicated capabilities of this fascinating technology.

### Motivation

Even though I've been working in a platform team at my organization for almost two years and have been working with Kubernetes since day one, prior to that I had very little knowledge of k8s. During this time, I learned everything on the fly, when it was necessary to complete a specific task. This was enough most of the time to set the tickets' statuses to done in Jira, but as soon as any kind of design choices were involved in the process, the gaps in my knowledge became blockers. I had to reach out to my team members and ask questions that made me feel dumb, since deep down I knew these are questions that I should already know the answers for. When I heard about the opportunity for taking the exam for “free”, I decided to fill up those gaps.

## Plan

I had to schedule the exam. Without being forced to study, I knew I was going to procrastinate. Looking at the calendar and seeing the number of remaining days going down is a great way to maintain motivation. I did some Googling to get a grasp of what to expect for the exam. There are a countless number of similar blog posts about this out there, so that was a good start. The majority of them mentioned and recommended a [course on Udemy](https://www.udemy.com/course/certified-kubernetes-administrator-with-practice-tests/) from Mumshad Mannambeth. Purchasing the course also gives you access to practice tests on Kode Kloud. Each topic covered by the course has its corresponding tests on Kode Kloud. On top of that, if you purchase the CKA program from the CNCF, you get access to their mock exam platform called killer.sh, but more on that later. That was pretty much it, that was my plan. Complete the course on Udemy, do the practice tests on Kode Kloud and finally try killer.sh. I did not want to overcomplicate things and if you are planning to take the exam as well, following my footsteps will most certainly give you the results that you are looking for.

## Thoughts on the course

Mumshad did a great job putting this course together. He explains everything in great detail and in a way that is easy to understand. The course is long, there are many videos that you need to go through, in order to cover all Kubernetes concepts. Since I was already familiar with the majority of the basic ones, I decided to speed things up and watch the videos at a 2x speed. If you can consume the information Mumshad shares at that pace, I recommend you do the same. This saves you a lot of time and leaves extra space for practicing. If that's too fast, take your time and don't stress about it. There's no rush, really. The practice tests on Kode Kloud were surprisingly simple. Watching the videos before taking these tests is enough to complete them without any major issues. You probably won't even need to look at the provided hints or solutions. In case you do, make sure you are not just copying and pasting whatever's on the screen, but actually understand the solution.

After completing every section in the course, there are three mock exams on Kode Kloud, that were created to mimic the real life exam. Although the environment is not the same, since the actual exam is on a remote desktop, the questions were somewhat similar to the ones in the real one, just a tiny bit simpler. It'll make you comfortable jumping between namespaces and contexts. When taking these tests, you should approach it the same way as you would during the actual exam. No distractions, no breaks. Do them multiple times until you can easily achieve 100%. Then do them a few more times again.

### tmux

You can use `tmux` to have multiple terminal sessions. I personally never used it and decided to not use it during the exam either, simply because of the lack of experience. If you don't know `tmux`, you don't have to start using it just for the CKA.

### .bashrc

There are a few things that might help you get through all the questions a lot quicker. I suggest you use these during each mock exams and the `killer.sh` as well. The more you practice, the faster you'll be able to set these up. The `alias k=kubectl` will be added by default, so no need to add that.

```
# Open .bashrc
vim ~/.bashrc

# Templating
export do='--dry-run=client -o yaml'

# Destroy resource immediately
export now='--grace-period 0 --force'

# Apply changes
source ~/.bashrc
```

With `$do` you will be able to generate template `yaml` which will be easily modifiable to your needs with `vim`:

```
k run test -n default --image=nginx $do > test.yaml
vi test.yaml
```


There's a chance that you'll have to delete pods, which might take longer than you think. To circumvent that, you can force them to be deleted instantly. You should not do this in a production environment, but for the CKA it is completely fine:

`k delete pod test $now`

## killer.sh

When you enroll in the CKA program, you automatically get two `killer.sh` runs. It is an environment which intended to replicate the real exam as much as possible. The only major difference between them is that `killer.sh` is not using a remote desktop. Both runs contain the same questions, and you can access each environment for 36 hours. There is a 2-hour timer to give you an idea of how long it should take to go through everything, but you can work on them for the entire 36 hours. There are a lot of questions, around 25, and they are way harder than the ones you'll face during the exam. This might scare you at first (it scared me at least), but don't get discouraged and still go through all the questions.

It took 4 hours for me to complete all the tasks and I managed to score around 70%. I did not even look at the solutions that day, since it was exhausting to focus 4 hours straight. The next day, I created a note and went through them. The solutions they provide are very detailed, so take your time and properly understand them. Take notes of the major topics that are being asked, since you'll get similar ones in the exam. Even though my score was not great, I still did not use my second run. I wanted to save it in case I fail my first attempt of the real exam.

## Exam

I decided to dedicate around 20 minutes before the exam to do the mock tests on Kode Kloud, just to get in the zone. Didn't even check the score, I only wanted to make my hands ready for all the `kubectl` commands.

When the exam starts and the `Take Exam` button becomes available on the portal, you will be prompted to download the PSI Secure Browser. This is a recent change in the exam process. There are many complaints about the browser, fortunately I had none. There is a self check-in where you have to show the proctor your environment. All of these are described in great detail [here](https://docs.linuxfoundation.org/tc-docs/certification/tips-cka-and-ckad). After the proctor approved everything, the actual exam starts.

If you went through all the `killer.sh` solutions and understood them properly, the questions in the real exam won't surprise you. They are way easier than `killer.sh`. You can flag the ones that you want to get back to at a later time. My suggestion would be to flag a question as soon as you feel stuck, since there are many easy questions at the end, too. Try to optimize your time as much as possible. Before each question, a command is provided which you can copy and paste to set the proper context. After 2 hours, the exam ends and the results will be sent via email after approximately 24 hours. I managed to pass with 88% on my first attempt! Unfortunately, they don't show you your mistakes, so you are out of luck if you plan to learn from them.

## Conclusion

While the exam turned out to be way easier than I initially expected, signing up for the CKA program was a great way to motivate myself to learn Kubernetes and become a pro user of the official documentation. Now I can perform tasks at my job with much higher confidence. Ever since I graduated from university, studying outside working hours was a struggle. Deciding to take this exam not only forced me to learn new things, but also increased my hunger for more. If you are planning to clear the CKA as well, following my path will probably give you the same result, as the picture shows below. Good luck!

![](./cka.png)
