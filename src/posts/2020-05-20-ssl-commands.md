---
title: SSL Commands
date: 2020-05-20T04:44:59.742Z
---
I've done this 3 times now, so I should be writing this down.

## Creating a CSR

```
openssl req -new -newkey rsa:2048 -nodes -keyout mobileapp.deped.gov.ph.key  -out mobileapp.deped.gov.ph.csr
```

## Creating an SSL bundle

An SSL bundle is required for Nginx which comprises of the provisioned certificate + intermediate certificates + root certificate

```
cat mobileapp_deped_gov_ph.crt DigiCertCA.crt > mobileapp.deped.gov.ph.ssl-bundle.crt
```


## Creating a .pfx file from .crt files

Azure requires a pfx file to add to the Application Gateway which will act as our SSL termination endpoint.

```
openssl pkcs12 -export -out mobileapp.deped.gov.ph.pfx -inkey ../mobileapp.deped.gov.ph.key -in mobileapp_deped_gov_ph.crt -certfile DigiCertCA.crt -certfile TrustedRoot.crt
```

## Completing the chain

So, it turns out I only needed DigiCertCA above, instead of including the root, as this breaks the intermediate chain certs. I think the last -certfile overrides the earlier call instead of chaining all the files.