# Pre-Lab

## ENGR account


ENGR account is different than your UCR NetID. It's not combination with number (tkim049, this is UCR NetID). If you never activate your ENGR account or you have an ENGR account but you forgot your password, then please visit [here](https://www.engr.ucr.edu/secured/systems/login.php) and create your one.


## ENGR X-windows systems access

The college provides three computational servers for student use both on and off campus. This computational servers provide our IC design toolchains.

To access these servers on Windows, you must first download and install an SSH client and an X Server.  Once you have finished downloading the links below, you may watch the Video Tutorial to see how to install and run these programs.

For OSX/Linux, you don't need to install as it's default software in these operating systems.

In the lab (WCH125), you can use PUTTY and you need to use with XMing.

We will use `storm.engr.ucr.edu` server thru SSH with X-forwarding service.

The Windows instruction can be found at [ here ](http://systems.engr.ucr.edu/tutorials/computational.html)

For more detail windows instruction for putty and Xming can be found at [ here ](http://www.geo.mtu.edu/geoschem/docs/putty_install.html)

For OSX/Linux, you can type following command in your terminal,

`ssh -Y [ENGRID]@storm.engr.ucr.edu`

For example

`ssh -Y tkim@storm.engr.ucr.edu`

If you have any question, then you can post your question at issue section in this github.

## Check Synopsys Galaxy Custom Designer

We already preconfigured every IC design environment, so you don't need to set any environment. You can check toolchain is correctly working.

`cdesigner&`
