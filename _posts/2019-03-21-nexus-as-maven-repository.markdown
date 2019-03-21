---
layout: post
title: "Nexus As Maven Repository"
categories: [nexus, maven]
tags: [nexus, maven, repository]
---

### What is Nexus?
{: style="text-align: justify"}
[Nexus](https://www.sonatype.com/nexus-repository-oss) is a tool from [Sonatype](https://www.sonatype.com/) that have function as repository for your binaries and artifacts. Nexus is a single source of truth for All your software parts. In this article, I will explain simple installation and configuration from nexus as Maven repository Server.

### Where We can find the software?
We can download software from [nexus-repository-oss](https://www.sonatype.com/nexus-repository-oss), We can choose the installer based on operating system that We have.

### Installation
Installation is just simple.
  - Extract file that You download.
  - Change directory into extracted folder.
  - run `bin/nexus run`
  - Open your browser and put the default nexus URL `http://your-ip-address:8081`

### Setting for Maven
add this code to your pom.xml
  ```
  <repositories>
      <repository>
          <id>releases</id>
          <name>releases</name>
          <url>http://your-ip-address:8081/repository/maven-releases/</url>
      </repository>        
      <repository>
          <id>snapshots</id>
          <name>Snapshots</name>
          <url>http://your-ip-address:8081/repository/maven-snapshots/</url>
      </repository>
  </repositories>
  ```
  Change `your-ip-address` with nexus ip address or nexus hostname

### Do you want publish your binary or library?
If yes, add this code to your pom.xml
```
  <distributionManagement>
    <repository>
        <id>releases</id>            
        <name>releases</name>
        <url>http://your-ip-address:8081/repository/maven-releases/</url>
    </repository>
    <snapshotRepository>
        <id>snapshots</id>
        <name>Snapshots</name>
        <url>http://your-ip-address:8081/repository/maven-snapshots/</url>
    </snapshotRepository>
  </distributionManagement>

```

Put Your nexus username and password in `.m2/settings.xml` at your project
```
  <settings xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.1.0 http://maven.apache.org/xsd/settings-1.1.0.xsd"
      xmlns="http://maven.apache.org/SETTINGS/1.1.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <servers>
      <server>
        <id>releases</id>
        <username>admin</username>
        <password>admin123</password>
      </server>
      <server>
        <id>snapshots</id>
        <username>admin</username>
        <password>admin123</password>
      </server>
    </servers>
  </settings>

```
default username/password is admin/admin123.

run `mvn deploy`, if success your library will show in release or snapshots repository, You can check this with Your browser.
