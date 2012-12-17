---
layout: post
title: "Lazy Developer's Toolbox #2 - Slightly Better Maven"
date: 2012-11-08 21:12
comments: true
categories: lazy toolbox mvn
---

I must admit I'm not really a huge fan of Maven, but I'm not going to rant how much _maven sucks_ in this post. This tool brought quite a bit of good things to the build automation landscape in Java. Instead I will share with you how to make it a bit more pleasant to use. It's still de facto a standard in open source world so I guess I will keep it in my toolbox for a little longer.

<!-- More -->

One of the concepts which is really handy is _profile_. But isn't it a bit annoying when you make a typo in the name to discover it only after the whole build is done? Wouldn't it be cool to have autocompletion in the command line? Something like:

```
$ mvn -P<TAB>
-Pglassfish-3.1-embedded           -Pjbossas-7.1-managed-mssql 
-Pjbossas-7.0-managed     
```

There is a simple way of enabling it in _bash_ - very nice [autocompletion script](https://github.com/juven/maven-bash-completion/). Run this commands then restart your shell. You will be few keystrokes ahead.

```
$ curl https://raw.github.com/juven/maven-bash-completion/master/bash_completion.bash >>  \
.maven_bash_completion.sh && echo 'source ~/.maven_bash_completion.sh' >> ~/.bashrc
```

### Pimp your Maven

Here's something extra (meaning it does not bring any value for lazy guys I guess). Maven is well known for being a chatterbox, next to its passion for downloading the whole internet once in a while. It would be pretty handy to mark failures in red, warnings in yellow and so on and so forth. This [_sed_ script](https://github.com/bartoszmajsak/maven-antsy-color/blob/master/mvn) will do the job. Run following snippet and enjoy the rainbow!

```
$ curl https://raw.github.com/builddoctor/maven-antsy-color/master/mvn >>  \
.maven_colorized.sh && echo 'source ~/.maven_colorized.sh' >> ~/.bashrc
```

If you have some other cool tips just leave a comment!
