# Making a headless zcash mining rig running *buntu

Firstly: If using *buntu, use 15.10 "Wily Werewolf". 15.10 is the latest *buntu version running a kernel that still supports Catalyst 15.12 through the binary blob `fglrx`. Later versions (e.g. 16.04 LTS) will give you the choice between running the open source `radeon` driver (bad/low results) or using the `AMDGPU-pro` drivers. If you are confident your mining rig will be populated exclusively by the handful of supported cards [listed on AMD's website](http://support.amd.com/en-us/kb-articles/Pages/AMD-Radeon-GPU-PRO-Linux-Beta-Driver%E2%80%93Release-Notes.aspx), go ahead and install 16.04 and `AMDGPU-pro`.

Also, I suggest you get [Lubuntu](http://lubuntu.net/) instead of the main Ubuntu flavour: Lubuntu has a lot less bloat, while still having a useful LXDE Desktop Environment for sorting out any hickups once you're on your new system. The aptly named [Ubuntu Mini Remix](http://www.ubuntu-mini-remix.org/) may be an alternative if you want to make your own, custom tailored *buntu live USB for mass deployment.

#### Creating the installation media

Get Lubuntu 15.10 [here](http://ftp.yzu.edu.tw/linux/ubuntu-cdimage/lubuntu/15.10/lubuntu-15.10-desktop-amd64.iso):
```sh
$ wget http://ftp.yzu.edu.tw/linux/ubuntu-cdimage/lubuntu/15.10/lubuntu-15.10-desktop-amd64.iso
```

Put the thing on the thing: 
```sh
$ dd bs=4M if=/path/to/lubuntu-15.10-desktop-amd64.iso of=/dev/sdX
$ sync
```

...where `/dev/sdX` is the device letter of your connected USB device, e.g. `/dev/sdc`. Don't use partition numbering, and  don't `dd` the drive your OS is running from. Do remember to `sync` before unplugging the USB from your computer.

#### Installing ubuntu

Upon booting the Lubuntu Live USB, install to the rig as normal. If using an USB as installation target, drop the swap, as having one may slow things down. Otherwise, go ahead as you would normally, but *opt for the automatic login* to your system.

After rebooting you should be logged in automagically to the LXDE desktop. Fire up a terminal and remove `light-locker`, unless you want your system locked at annoying intervals:
```sh
$ sudo apt-get -y remove light-locker*
```

Optionally, continue with removing unnecessary bloat:
```sh
$ sudo apt-get -y remove abiword audacious* cups* galculator gnome-mplayer gnumeric pidgin sylpheed* transmission xfburn
```

Now, install fglrx:
```sh
$ sudo apt-get install fglrx-updates
```
Reboot.

After rebooting, run ATI's intial configuration:
```sh
$ sudo aticonfig --adapter=all --initial
```

Now reboot again.

After rebooting, you may confirm that aticonfig finds all your cards:
```sh
$ sudo aticonfig --lsa
```

Your system should now be ready to set up a miner application.

#### Setting up Claymore's Zcash Miner for Linux

Install and set up Claymore's Zcash miner for linux. Links are found [here](https://bitcointalk.org/index.php?topic=1670733.0). Download the tarball and extract it with
```sh
$ mkdir ~/ClaymoreZEC && tar xzvf /path/to/Claymores_ugly_and_long_named_tarball_vXX.tar.gz  -C ~/ClaymoreZEC --strip-components 1
```

If you want to test run the miner, Claymore advises to export some environment variables before you run it, "especially if you have 1-2GB cards". On my setup, it seems that whether the first variable is 0 or 1 doesn't matter. YMMV:
```sh
$ export GPU_FORCE_64BIT_PTR=1
$ export GPU_MAX_HEAP_SIZE=100
$ export GPU_USE_SYNC_OBJECTS=1
$ export GPU_MAX_ALLOC_PERCENT=100
$ export GPU_SINGLE_ALLOC_PERCENT=100
```
(You'll add these lines to `~/.profile` for persistancy later in the walkthrough, though)

After finding your preferred settings for the miner, set these in `config.txt`
```sh
$ nano ~/ClaymoreZEC/config.txt
```
Refer to the internets and the `~/ClaymoreZEC/README\!\!\!.txt` for tinkering with the miner's settings.

#### Automation: ~/.profile

Using the `~/.profile` file will cause commands to execute every time you log in as the associated user. @asbjornenge will have a better way.
```sh
$ nano ~/.profile
```

Add the following lines at the bottom:

```
export GPU_FORCE_64BIT_PTR=1
export GPU_MAX_HEAP_SIZE=100
export GPU_USE_SYNC_OBJECTS=1
export GPU_MAX_ALLOC_PERCENT=100
export GPU_SINGLE_ALLOC_PERCENT=100

sleep 10
xterm -e ~/ClaymoreZEC/zecminer64
```

From [DrMrLordX's post](https://forums.anandtech.com/threads/zcash-zec-gpu-mining.2490229/page-5#post-38558544) on the AnandTech forums:
>"Every time you start up the account with that particular text in its .profile file in its home directory, that stuff gets executed BEFORE loading the desktop environment. The net effect is that you get a single xterm running the SilentArmy miner without any desktop. The desktop will not load until you kill the xterm. Just mouse over it (you will have a mouse cursor), left-click to make sure you have the term selected, and then hit Ctrl-C to kill the xterm. Then the desktop environment will load normally. Even if you kill the xterm, the environment variables set in your .profile will still enable mining with 2 Gb cards, [...] so you can always manually open up a terminal and execute [zecminer64] by hand to resume mining.
Reboot your machine and watch what happens. If it starts mining in a tiny little term window against a black screen, you're in there! Now you can shut down the machine, disconnect the monitor, and reboot and mine with headless confidence."

Our Lord @asbjornenge will make this better. And he will replace every instance of `nano` with `vim`. `leafpad` is a great little editor that is the standard in LXDE. HYOH.
