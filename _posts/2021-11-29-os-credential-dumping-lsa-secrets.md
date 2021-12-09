---
layout: single
title:  "OS Credential Dumping: LSA Secrets"
date:   2021-11-29
categories: CredentialAccess CredentialDumping
sidebar:
    nav: "credaccess"
toc: true
---

# Introduction
 Copy Pasta for Verbage length:

Adversaries with SYSTEM access to a host may attempt to access Local Security Authority (LSA) secrets, which can contain a variety of different credential materials, such as credentials for service accounts.[1][2][3] LSA secrets are stored in the registry at HKEY_LOCAL_MACHINE\SECURITY\Policy\Secrets. LSA secrets can also be dumped from memory.[4]

Reg can be used to extract from the Registry. Mimikatz can be used to extract secrets from memory.[4]

# Cheatsheet
Secrets Dump:
{% highlight linux %}
secretsdump.py 
{% endhighlight %}


# How This Works
# References & Links
1. [https://attack.mitre.org/techniques/T1003/004/](https://attack.mitre.org/techniques/T1003/004/)
