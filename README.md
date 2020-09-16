# speak2pc

Control your PC with your phone by voice.

To get voice control running on my Linux laptop proved to be a mess. Running
voice control on my Android phone was a breeze. Connecting the two is
rudimentary. So now I can talk to my phone while on stage and the right
presentation pops up on my laptop that sits on the otheer side of the stage.
Or any other creative scenario you may imagine.

Here is a video to show how this works:

[![Shepherd Harvest Design Sprint](/img/speak2pc.png)](https://youtu.be/XNkNfWF5Uk0 "Speak2PC")

## Prerequisite

You need a phone running [Termux]() with the packages `termux-tts-speak` and
`termux-speech-to-text` installed. You also need the packages `Ruby` and
`OpenSSL`. Use `pkg install` inside termux to install these packages.

Generate ssh keys on your phone and upload them to your PC running `sshd`
and accepting ssh connection. Unless you have a static IP on your PC, both
devices must be connected to the same local wifi network. This may well work
on a Windows or Mac PC. I have only tested this on Linux and with an Android
phone.

In order to not have to enter your password when connection to your PC (or
worse - say it aloud), you upload the ssh keys from your phone to your PC like
this:

```
cat ~/.ssh/id_rsa.pub | ssh user@192.168.0.2 "cat >> ~/.ssh/authorized_keys"
```
Replace "user" with your user on the PC and "192.168.0.2" with the actual IP
address of your PC.

You need the program `Android/pc` running on your phone and the program
`PC/remotescript` running on your pc.

## Running the setup

Start the program `pc` on your phone and listen to the woman's gentle voice
saying "My love, where do you want to go today?". You answer back with the IP
address of your PC. If you have previously given her the IP address and want
to connect to the same, simply answer her "The same as last time, dear" (or
indeed any sentence containing the word "same". Note that the list sound you
make will not be captured, so you need to add a word at the end of the
address, such as "192 168 0 2 done" and the program will capture you voice and
translate that to "192.168.0.2".

The lady will then say "Your wish is my command", at which point you can add a
command that will be given as a parameter to the program that will be run on
the PC (the `remotescript` program). This parameter can be anything, but I
have chosen to use a number above 100 as a code (see `remotescript`). If you
give no parameter or a parameter unknown to `remotescript`, it will be
disregarded and the default action will be run (again see `remotescript`).

After the action on the PC is completed, the lady will end off with "Thank you
for the pleasant connection."

Tweak this as you wish and enjoy talking to the nice lady.
