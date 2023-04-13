# Mikrotik-Blacklist
This is a blocklist I use with on my Mikrotik router to block all connections from known spam/criminal/etc. networks.

Every couple days I pull lists from:
- Spamhaus (DROP & EDROP)
- dShield  
- blacklist.de (all.txt)
- Feodo
- pfSense lists

and reformat it to allow automatic import to MT routers. This is automated process so if you see errors in the final list open an issue please.

# READ THIS BEFORE GOING ANY FORWARD!

As of April 2023 blocklist has almost 5MB, installing this on a device with low disk space, such as HeX PoE, may (and almost certainly will) cause issues such as inability to save other settings if disk is full. You have been warned.

## How to run this on MT
Run following to your MT device with not less that 7d schedule (sources are not updated more frequently anyway):  

Download script:  
`/tool fetch url="https://raw.githubusercontent.com/pwlgrzs/Mikrotik-Blacklist/master/blacklist.rsc" mode=https`  
Install script:  
`/ip firewall address-list remove [find where list="pwlgrzs-blacklist"]; /import file-name=blacklist.rsc`

You'll also need firewall rule:  
`/ip firewall filter add chain=input action=drop connection-state=new src-address-list=pwlgrzs-blacklist in-interface=IFNAME`  
*Note: Replace IFNAME in-interface name with one you have configured*

Check out more detailed instructions [here](https://pawelgrzes.pl/posts/Mikrotik-Blocking-unwanted-connections-with-external-IP-list/).

You can also import install.rsc file, it will do all of above for you.  
Upload to MT and run `/import file-name=install.rsc` in terminal. You still need to manually add firewall rule.

## TODO
 - Add more sources.
