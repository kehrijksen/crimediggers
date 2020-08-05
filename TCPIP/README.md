### Assignment
We have intercepted network traffic related to an online scam case. Can you find out if malware has been sent?

### Mail traffic
We load the pcapng file into Wireshark and go to "File" -> "Export Objects" -> "IMF..." and find the following e-mails when using "Follow" -> "TCP Stream":

Packet \#4670
> To: z3r0b3t404@gmail.com
From: jimhendraxx <jimhendraxx@snel-adsl.nl>
Subject: Ransomware
Date: Wed, 24 Apr 2019 13:24:59 +0200
Hey I saw your ransomware on the darkweb and wanted to buy it, what do I 
need to do?

Packet \#5901
> To: jimhendraxx@snel-adsl.nl
From: z3r0b3t404 <z3r0b3t404@gmail.com>
Subject: Plan
Date: Fri, 24 Apr 2019 13:28:09 +0200
I'll send you the malware as soon as I recieve the listed amount in my bitcoin wallet.

Packet \#6061
> To: z3r0b3t404 <z3r0b3t404@gmail.com>
From: jimhendraxx <jimhendraxx@snel-adsl.nl>
Subject: Re: Plan
Date: Wed, 24 Apr 2019 13:29:37 +0200
Alright I've sent you the money

Packet \#6125
> To: jimhendraxx@snel-adsl.nl
From: z3r0b3t404 <z3r0b3t404@gmail.com>
Subject: ransom
Date: Fri, 24 Apr 2019 13:30:34 +0200
Thanks for the bitcoins

>--=_d01b10f6f290a4cbcdabba0a6429ed14
Content-Transfer-Encoding: base64
Content-Type: application/zip;
 name=Z3r0b3t4.zip
Content-Disposition: attachment;
 filename=Z3r0b3t4.zip;
 size=228

>UEsDBDMDAQBjAJVgmE4AAAAAOAAAACQAAAAIAAsAWjNyMGIzdDQBmQcAAgBBRQEAAAar8f0CJH0b
0dRIZM21W8X3QBvYXHkbbRcPRri6nWSxmPXDZROI9vjScAQ0ES3wrtOI2IvsuyYhUEsBAj8DMwMB
AGMAlWCYTgAAAAA4AAAAJAAAAAgALwAAAAAAAAAggLSBAAAAAFozcjBiM3Q0CgAgAAAAAAABABgA
gEIVIoX61AGAQhUihfrUAYBCFSKF+tQBAZkHAAIAQUUBAABQSwUGAAAAAAEAAQBlAAAAaQAAAAAA
--=_d01b10f6f290a4cbcdabba0a6429ed14--

Packet \#14450
> To: z3r0b3t404 <z3r0b3t404@gmail.com>
From: jimhendraxx <jimhendraxx@snel-adsl.nl>
Subject: Re: ransom
Date: Wed, 24 Apr 2019 13:34:09 +0200
hey man I got the ransomware but I can't open it, it tells me that I 
need a password...

Packet #14798
> To: jimhendraxx@snel-adsl.nl
From: z3r0b3t404 <z3r0b3t404@gmail.com>
Subject: ...
Date: Fri, 24 Apr 2019 13:36:45 +0200
The password for the zip is 5Jsg23Po%q12

### HTTP traffic
Before around packet \#4000 we can see the target looking up whether it is illegal to extort his employer, and where to get ransomware.
After around packet \#6000 we can see the target looking up how to decrypt .zip files.

### Malware
We can see an attachment: **Z3r0b3t4.zip** being sent along with a password. Using a [Base64 to binary converter](https://base64.guru/converter/decode/file "Base64 to binary converter") we can reconstruct the .zip file, filling in:
`UEsDBDMDAQBjAJVgmE4AAAAAOAAAACQAAAAIAAsAWjNyMGIzdDQBmQcAAgBBRQEAAAar8f0CJH0b
0dRIZM21W8X3QBvYXHkbbRcPRri6nWSxmPXDZROI9vjScAQ0ES3wrtOI2IvsuyYhUEsBAj8DMwMB
AGMAlWCYTgAAAAA4AAAAJAAAAAgALwAAAAAAAAAggLSBAAAAAFozcjBiM3Q0CgAgAAAAAAABABgA
gEIVIoX61AGAQhUihfrUAYBCFSKF+tQBAZkHAAIAQUUBAABQSwUGAAAAAAEAAQBlAAAAaQAAAAAA`

Using 7zip we open the .zip file, filling in the password `5Jsg23Po%q12`, and find the following file: Z3r0b3t4. Opening it shows the following text:
> Thanks voor de bitcoins! #SUCKAHHHH

### Conclusion
It seems like the target was looking to extort his employer with ransomware, bought it from z3r0b3t404 and then got scammed.