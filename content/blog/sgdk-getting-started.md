---
title: Getting Started Setting Up Sega Genesis Development on macOS
date: 2023-05-11
description: >-
  SGDK is an open-source Sega Genesis / Mega Drive SDK that allows for software to be written in C for the Sega Genesis. In this post we will be going over on how to set up your first project on macOS.
cover: >-
  img/sgdk-getting-started/1.webp
---

I recently tried to start developing a prototype game for the Sega Genesis and found that there was not many guides for using macOS when developing with SGDK, most of the posts and tutorials I found were using either Windows or Linux. So I tried testing some methods to get the best setup for developing with SGDK on macOS and in this post I will share the method I have found to work best.

## Lets Get Started

You will need some boilerplate to create a SGDK project, this can be done by using the simple [retrodevhelper](https://github.com/studioripe/retrodevhelper) tool, this can be installed by running the following scripts which will depend on [Homebrew](https://brew.sh) being installed.

```bash
brew tap studioripe/retrodevhelper
brew install retrodevhelper
```

Once the tool has been installed you can run the simple command `retrodevhelper init` which will guide you through the process of creating the boilerplate, make sure your settings match the image below and it will create the structure needed for this project.

![Starting a new project in retrodevhelper](/img/sgdk-getting-started/2.webp)

## Containers?

At first I thought about compiling SGDK to work with macOS and then I found the great [SGDK docker images by doragasu](https://gitlab.com/doragasu/docker-sgdk) that work great and simplify the whole installation process to just using Docker. Docker allows for the building of the game to happen inside an image which means no random SDKs or hard to configure environments need to be installed on your computer. It does this by running images like the doragasu SGDK one inside a container that allows for a much easier development environment setup.

Now to begin we will need to install docker desktop which is simple and can be done by going to [https://www.docker.com](https://www.docker.com/) and downloading and installing Docker Desktop for your architecture. Once that is done you should be able to open the docker application and follow the prompts until you end up at a screen that looks like this with the docker daemon running.

![Docker desktop running correctly](/img/sgdk-getting-started/3.webp)

## Too Many Commands…

Now if you looked at the link above for the docker image you would have seen a command that looked like the one below.

```bash
docker run --rm -v $PWD:/m68k -t registry.gitlab.com/doragasu/docker-sgdk:v1.80
```

If you thought that's too long to remember every time you want to run a build well then your in luck as retrodevhelper will help with this too, it allows you to run the simple command `retrodevhelper build` instead of the large one above. Go ahead and run this command in the project directory you created earlier and you will hopefully see that it is completed successfully and there is now a file called rom.bin in the output directory. In the next step we will go through the mess that is finding a emulator that actually works on the latest version of macOS.

![The generated files](/img/sgdk-getting-started/4.webp)

## Can I See it Working?

It seems like every Sega Genesis emulator on macOS is designed for playing games instead of development and the ones designed for development don’t work on modern versions of macOS. At first I tried looking for a macOS build of Gens but that didn't exist and then I tried the macOS version of blastem on a M1 mac and it would crash when booting up a game. I then tried openEMU but that kept asking to add it to the library on boot, in the end I found the emulator [Genesis Plus](https://www.bannister.org/software/gplus.htm) which seems to work fine on macOS. It doesn't have the debugging features of the other emulators but can be launched from terminal which makes it easy for development.

To run the generated rom.bin file, download Genesis Plus from the link above and install it into the applications folder, once this is done run the command `retrodevhelper run` which will start up Genesis Plus and should show “Hello World!” on the screen.

![Game running on the emulator](/img/sgdk-getting-started/5.webp)

Now your project should be in a state where you can add whatever you want and make that classic game you’ve always wanted to make. If you have any questions about this post feel free to leave a comment and if there are any features you think should be in retrodevhelper feel free to create an issue or leave feedback at [https://github.com/studioripe/retrodevhelper](https://github.com/studioripe/retrodevhelper).
