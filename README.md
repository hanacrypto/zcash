# Zcash Mining

Currently we are mining [zcash](https://z.cash/) in the [flypool](http://zcash.flypool.org/).
Miner status [here](http://zcash.flypool.org/miners/t1cdYQaJCYEEc5DrGoVfa6WJM7PLzGe6m6J).

Wallet address: t1cdYQaJCYEEc5DrGoVfa6WJM7PLzGe6m6J

## GPU Mining AMD/Radeon, Linux

[Install Instructions](https://github.com/hanacrypto/zcash/blob/master/lubuntu_mining.md).

## CPU Mining Linux

[Install Instructions](https://github.com/etherchain-org/nheqminer).

```
./nheqminer -l eu1-zcash.flypool.org:3333 -u t1cdYQaJCYEEc5DrGoVfa6WJM7PLzGe6m6J.<nodename> -p <random password> -t <num_threads>
```

## CPU Mining Windows 

[Download](https://github.com/etherchain-org/nheqminer/releases/tag/0.2).

Use `cmd.exe` (command line) to execute the below command.

```
nheqminer.exe -l eu1-zcash -u t1cdYQaJCYEEc5DrGoVfa6WJM7PLzGe6m6J.<nodename>
```

## GPU Mining Nvidia (Windows)

[Download](https://github.com/etherchain-org/nheqminer/releases/tag/0.2).

Use `cmd.exe` (command line) to execute the below command.

```
nheqminer.exe -cd 0 -l eu1-zcash -u t1cdYQaJCYEEc5DrGoVfa6WJM7PLzGe6m6J.<nodename>
```

The `-cd` parameter refers to the display adapter DeviceID, or whatever the `nheqminer` thinks it is. Start with 0 and then try 1 etc. until you succeed.

## GPU Mining AMD/Radeon (Windows)

[Download](https://github.com/Genoil/ZECMiner/tree/master/releases)

Use `cmd.exe` (command line) to execute the below command.

```
genoil.exe -c eu1-zcash.flypool.org:3333 -u t1cdYQaJCYEEc5DrGoVfa6WJM7PLzGe6m6J.<nodename> -p <random_password>
```

## Restart scripts for Windows

Sometimes the windows miners halt. Typically the GPU miners. Here are some script to help autorestart.

`autorestart.bat`

````
:loop1
start start.bat
timeout /T 3600
taskkill /F /IM genoil.exe
timeout /T 25
goto loop1
```

`start.bat`

```
<minig_cmd_from_above>
exit
```

Make two files, `autorestart.bat` and `start.bat`. `start.bat` is the batch file for running the miner. `autorestart.bat` is the batch file is for restarting miner within a certain time interval. It is set as 1 hour (3600 seconds) in the example above. Feel free to adjust that numbers between 1800 ~ 7200

enjoy.
