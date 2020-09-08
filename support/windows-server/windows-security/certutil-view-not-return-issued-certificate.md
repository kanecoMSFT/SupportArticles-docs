---
title: Certutil -view doesn't return issued certificates
description: Fixes an issue where the Certutil -view command doesn't return issued certificates correctly.
ms.date: 09/08/2020
author: delhan
ms.author: Delead-Han
manager: dscontentpm
audience: itpro
ms.topic: troubleshooting
ms.prod: windows-server
localization_priority: medium
ms.reviewer: kaushika
ms.prod-support-area-path: Certificates and public key infrastructure (PKI)
ms.technology: WindowsSecurity
---
# "Certutil -view" command does not return issued certificates correctly

This article provides help to fix an issue where the `Certutil -view`command doesn't return issued certificates correctly.

_Original product version:_ &nbsp; Windows Server 2012 R2  
_Original KB number:_ &nbsp; 2233022

## Symptoms

The Certutil command-line tool can be used to display the certificates that have been issued by a certification authority using the `-view` parameter. Under some circumstances, Certutil may not display all the expected certificates. 

For example, the following command would not return the expected number of certificates:

**certutil -view -restrict "RequesterName=contoso\twt"**  

Output would be similar to the following:

> Maximum Row Index: 0  
0 Rows  
0 Row Properties, Total Size = 0, Max Size = 0, Ave Size = 0  
0 Request Attributes, Total Size = 0, Max Size = 0, Ave Size = 0  
0 Certificate Extensions, Total Size = 0, Max Size = 0, Ave Size = 0  
0 Total Fields, Total Size = 0, Max Size = 0, Ave Size = 0  
CertUtil: -view command completed successfully.

## Cause

This issue is a result of how Certutil handles parsing for the -view parameter. Specifically, there is an issue with how it parses the following escape characters: \n , \r, and \t.

## Resolution

The workaround is to uppercase all requester name strings passed as restrictions on the Certutil command line.

For example, instead of using this command:

**certutil -view -restrict "RequesterName=contoso\twt"**  
Use this command:

**certutil -view -restrict "RequesterName=contoso\TWT"**