## Configure touchpad tapping
```console
~/.scripts/xfce_autostart.sh
    synclient TapButton1=1 TapButton2=2 TapButton3=3

xinput list
xinput list-props ...
xinput set-prop ...
```
Then in "Session and Startup" -> "Application Autostart" -> Add ```~/.scripts/xfce_autostart.sh```

## Install ```redshift```
```console
$ cat ~/.config/redshift.conf # in dom0
[redshift]
temp-day=5700
temp-night=3600
gamma=0.8
adjustment-method=randr
location-provider=manual

[manual] 
lat=49.41
lon=5.49

startup script:
#!/bin/sh
sleep 2
redshift
```
Then "Session and Startup" -> "Application Autostart" -> Add ```redshift```

## Make calendar week start on Monday
On dom0 in ```~/.profile````:
```console
export LC_TIME="en_GB.UTF-8"        # date format (still English, but weeks start on monday)
```

## Copy files from domU to dom0
```console
$ qvm-run --pass-io <src-qube> 'cat /path/to/file_in_src_qube' > /path/to/file_name_in_dom0
```

## ```netcat``` between Qubes

```console
# on personal
$ qvm-connect-tcp 1234:work:2345
Binding TCP 'work:2345' to 'localhost:1234'...

# on dom0
$ cat /etc/qubes-rpc/policy/qubes.ConnectTCP:
from    to  action
personal    work    allow
@anyvm      @anyvm  deny

# on work:
$ nc -l -p 2345

# on personal:
$ nc localhost 1234
```

## LibreOffice smooth scrolling
https://rudd-o.com/linux-and-free-software/making-libreoffice-run-at-an-acceptable-speed-under-qubes-os
```console
$ export SAL_USE_VCLPLUGIN=kf5
$ sudo apt install libreoffice-kf5
```

## Repair DNS after network connection juggling

```console
$ sudo /usr/lib/qubes/qubes-setup-dnat-to-ns
```

## Expose a local webserver
On the webserver qubes (10.137.0.25):
```console
$ sudo nft 'insert rule qubes custom-input iifname eth0 tcp dport {80, 443} accept'
```
On sys-net:
```console
$ sudo nft 'add chain qubes prerouting-nat { type nat hook prerouting priority -100; }'
$ sudo nft 'add rule qubes prerouting-nat iif ens7 tcp dport { 80, 443 } dnat to 10.137.0.25'
$ sudo nft 'add rule qubes prerouting-nat iif wls6f0 tcp dport { 80, 443 } dnat to 10.137.0.25'
- sudo nft 'insert rule qubes custom-forward iifname ens7 tcp dport {80, 443} accept'
- sudo nft 'insert rule qubes custom-forward iifname wls6f0 tcp dport {80, 443} accept'
```
## Unsolved issues
+ Sleep mode (S0ix) on Lenovo T14 gen 4
	+ https://github.com/QubesOS/qubes-issues/issues/6411
+ Screensaver and USB keyboard
	+ Password starting with a shift key
	+ https://github.com/QubesOS/qubes-issues/issues/9603
