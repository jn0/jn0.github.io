# Powercom BNT-1200AP

`/etc/nut/nut.conf`
```
MODE=standalone
UPSD_OPTIONS="-a pcmbnt1200ap"
UPSMON_OPTIONS=""
```

`/etc/nut/ups.conf`
```
maxretry = 3

[pcmbnt1200ap]
        driver = usbhid-ups
        port = auto
        desc = "Powercom BNT-1200AP"
        vendorid = 0d9f
        productid = 00a6
```

`/etc/nut/upsmon.conf`
```
MONITOR pcmbnt1200ap@localhost 1 upsmon pass master
MINSUPPLIES 1
SHUTDOWNCMD "/sbin/shutdown -h +0"
POLLFREQ 5
POLLFREQALERT 5
HOSTSYNC 15
DEADTIME 15
POWERDOWNFLAG /etc/killpower
RBWARNTIME 43200
NOCOMMWARNTIME 300
FINALDELAY 5
```

This works fine: `sudo /lib/nut/usbhid-ups -DDDD -a pcmbnt1200ap`

But it doesn't work in whole :(

- [config talks @LOR](https://www.linux.org.ru/forum/linux-hardware/12903216)
- [config talks @habr](https://habr.com/post/246671/)
- [config study](http://www.muff.kiev.ua/content/nut-network-ups-tools)
- [The NUT](https://sites.google.com/site/plan0metr/home/nut)
- [Photos of internals](https://imgur.com/a/iHTfS)
- [PCM FAQ](http://pcm.ru/support/faq/)
- [PCM Software 1](http://pcm.ru/support/soft/)
- [PCM Software 2](https://www.pcm-ups.eu/en/software-app/)
