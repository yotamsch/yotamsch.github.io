---
layout: post
title: "Getting Started With Java Development On Linux"
author: "Yotam S"
categories: guide
tags: [java, linux, tutorial]
image: "/2018-4-23/post-image.png"
---
[Java](https://en.wikipedia.org/wiki/Java_(programming_language)) is a widely used object oriented language. And more over you could do Java programming basically everywhere! In this little tutorial I will try and guide you with installing Java on your Linux environment.

## The set-up
I'm using a [Lubuntu](https://lubuntu.net/) 17.10 (64 Bit) virtual machine, installed with [VirtualBox](https://www.virtualbox.org/). Lubuntu is one of the smaller distro's based on Ubuntu. Therefore it is also compatible with `sudo apt-get` and all the Ubuntu repositories. Out of the box there are still some things you should install before getting started. I recommend running the following set of commands:
```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install gcc make build-essential
```
And remember to install the VirtualBox Guest additions for better integration.

__Note:__ If you are using a non Latin based locale as me (can check with the shell command `locale`), it is good practice to declare it UTF-8. In my case I had to run the command:
```bash
sudo update-locale LANG=en_IL.UTF-8
```

## Installing Java
I'll be installing Java 8 but you may choose any other version you prefer. Check out  the [documentations](https://docs.oracle.com/javase/10/) for information on other versions. It's very easy to install Java on Linux, the commands I use are for Ubuntu based machines but the change to other distros is easy. Just replace the package manager part to your distro's. First we want to install Java itself. Use the following commands:

```bash
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
sudo apt-get install oracle-java8-set-default
```
Follow the on-screan instructions and execute the installation. After the installation is complete let's check that Java was install correctly. Java has both an interpreter and a compiler, so we should check for both. Execute the following commands and see that the returned values are correct:


```bash
javac -version # checks the compiler version
java -version # checks the interpreter version
```

## Installing an IDE
With Java development, I enjoy working with the [Eclipse IDE](http://www.eclipse.org/). But there are many more options, such as the open source [NetBeans IDE](https://netbeans.org/), [IntelliJ IDEA](https://www.jetbrains.com/idea/), [Visual Studio Code](https://code.visualstudio.com/) and more! Choose the one you like best. For Eclipse, to get the newest version we would be compiling from source. Lucky for us, in Ubuntu we have [`ubuntu-make`](https://wiki.ubuntu.com/ubuntu-make) that basically does all the heavy lifting for us! Use the following commands to install it:

```bash
sudo add-apt-repository ppa:ubuntu-desktop/ubuntu-make
sudo apt update
sudo apt install ubuntu-make
```

Follow the on screen instructions and execute the install, it shouldn't take long. Now, after that's installed, we want to install Eclipse with it. Execute the following command to install Eclipse for Java development:

```bash
umake ide eclipse
```

You will be promped to choose an install location. For comfort I recommend installing it in `/home/YOUR-USERNAME/.local/share/eclipse`. Using `ubuntu-make` will install all needed dependencies and also handle a start menu shortcut for you. What a treat! If after installation you don't see any shortcut in the start menu, just use the following command to copy the file into the needed directory:

```bash
sudo cp ~/.local/share/applications/eclipse-java.desktop /usr/share/applications/.
```

And that's it, now you have a brand new fully functional Java development environment!

# Your "Hello World" program
Start up Eclipse and you'll be greeted with the welcome screen. Pressing the tiny button on the left side of the screen (see below image) will switch to the project view.
![java project view button]({{ site.baseurl }}/assets/img/2018-4-23/java-open-java-view.png "Switching to the project view")

Don't forget to create a new project, go to `File->New->Java Project`. We will call our project `hello-world` as you probably have guessed. Your project creation window should look similar to mine.
![java project creation]({{ site.baseurl }}/assets/img/2018-4-23/java-create-project-hello-world.png "Creating a project in Java")

After your project was created, right-click the `/src` folder under your project branch (on the left panel) and select `New->Class`.
![java new class]({{ site.baseurl }}/assets/img/2018-4-23/java-new-class-1.png "Creating a class in Java")

Give it a name and package (optional, you may leave it empty) and press finish!
![java new class]({{ site.baseurl }}/assets/img/2018-4-23/java-new-class-2.png "Creating a class in Java")

Place the following `main` function inside the class you just created. And **Run** your code.

```java
public static void main(String[] args) {
		System.out.println("I\'m so excited...");
		System.out.println("I just can't hide it!");
		System.out.println("Oh yeah... Hello World.");
}
```

And the output which shows in the `Console` should be:
```
I'm so excited...
I just can't hide it!
Oh yeah... Hello World.
```

And Vualla, you have created your first Java program <i class="fa fa-smile-o" aria-hidden="true" />

## Conclusion
I hope I was able to help you get a generall idea of Java programming on Linux and maybe even get you started. Installing Java and an accompanying IDE is very easy on Linux so don't be afraid to try. Enjoy your Java development!
