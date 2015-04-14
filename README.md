# ipset-persistent

## Use cases

The main use-case for this script - is to use it with `iptables-persistent` package. If you use sets in your iptables rules - sets should be loaded **before** this rules. This scripts declares dependencies for dependency-based booting - it starts before iptables-persistent and recreates all sets.

## Installation

### Manual

Clone repository to some directory:

```
cd /home/username
git clone https://github.com/soar/ipset-persistent.git ./
```

Copy files to system:

```
sudo cp --parent etc/ipset/README /
sudo cp --parent etc/default/ipset-persistent /
sudo cp --parent etc/init.d/ipset-persistent /
```

Add to autostart:

```
sudo update-rc.d ipset-persistent defaults
```

## Usage examples

For example: create set and rule:

```
ipset create testset hash:net
iptables -A INPUT -m set --match-set testset src -j ACCEPT
```

Save it:

```
service ipset-persistent save
```

Now all sets will be recreated after system reboot.
