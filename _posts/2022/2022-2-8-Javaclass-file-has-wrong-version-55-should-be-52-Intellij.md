---
layout: post
title: "Java IntelliJ error-class file has wrong version 55.0, should be 52.0"
date: 2022-2-8
categories:
  - Java
tags:
  - Java
  - IntelliJ
---

**Use case**
During run ./gradlew clean build, it returns below error


```
class file has wrong version 55.0, should be 52.0
Please remove or make sure it appears in the correct subdirectory of the classpath.
```

**Problem**

This error indicates the java version is not correct. version 55 means Java 11 and version 52 means Java 8.

**Solution**

1) In this situation, should go to IntelliJ >> File >> Project Structure

![001](/assets/image/2022-2-8/2022-2-8-Javaclass-file-has-wrong-version-55-should-be-52-Intellij_001.png)  

make sure all the JVM settings are pointing to the right version.

2) Clear gradle cache
```
rm -r $HOME/.gradle/caches/
```

Once above steps are done, then run ./gradlew clean build. This problem should be fixed.
