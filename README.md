# Zcash Mining

Currently we are mining [zcash](https://z.cash/) in the [flypool](http://zcash.flypool.org/).
Miner status [here](http://zcash.flypool.org/miners/t1Yw8f7mzpqw3LhsHCEhWZwQa6CDzErJzrx).

## CPU Mining Linux

[Install Instructions](https://github.com/etherchain-org/nheqminer).

```
./nheqminer -l eu1-zcash.flypool.org:3333 -u t1Yw8f7mzpqw3LhsHCEhWZwQa6CDzErJzrx.<nodename> -p <random password> -t <num_threads>
```

## CPU Mining Windows 

[Download](https://github.com/etherchain-org/nheqminer/releases/tag/0.2).

Use `cmd.exe` (command line) to execute the below command.

```
nheqminer.exe -l eu1-zcash -u t1Yw8f7mzpqw3LhsHCEhWZwQa6CDzErJzrx.<nodename>
```

## GPU Mining Nvidia (Windows)

[Download](https://github.com/etherchain-org/nheqminer/releases/tag/0.2).

Use `cmd.exe` (command line) to execute the below command.

```
nheqminer.exe -cd 0 -l eu1-zcash -u t1Yw8f7mzpqw3LhsHCEhWZwQa6CDzErJzrx.<nodename>
```

The `-cd` parameter refers to the display adapter DeviceID, or whatever the `nheqminer` thinks it is. Start with 0 and then try 1 etc. until you succeed.

## GPU Mining AMD/Radeon (Windows)

[Download](https://github.com/Genoil/ZECMiner/tree/master/releases)

Use `cmd.exe` (command line) to execute the below command.

```
genoil.exe -c eu1-zcash.flypool.org:3333 -u t1Yw8f7mzpqw3LhsHCEhWZwQa6CDzErJzrx.rig1 -p <random_password>
```

enjoy.
