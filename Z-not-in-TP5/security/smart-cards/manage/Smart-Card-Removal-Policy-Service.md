---
title: Smart Card Removal Policy Service
ms.custom: na
ms.prod: windows-server-2012-r2
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-security
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a4799375-14b4-42f0-b83f-c1ac65dd61dc
---
# Smart Card Removal Policy Service
This topic for the IT professional describes the role of the removal policy service \(ScPolicySvc\) in smart card implementation.

The smart card removal policy service is applicable when a user has signed in with a smart card and subsequently removes that smart card from the reader. The action that is performed when the smart card is removed is controlled by Group Policy settings. For more information, see [Smart Card Group Policy and Registry Settings](smart-card-tools-and-settings/Smart-Card-Group-Policy-and-Registry-Settings.md).

**Smart card removal policy service**

![](../../media/Smart-Card-Removal-Policy-Service/WindowsSmartCardTechnicalReference_07.gif)

The numbers in the previous figure represent the following actions:

1.  Winlogon is not directly involved in monitoring for smart card removal events. The sequence of steps that are involved when a smart card is removed begins with the smart card credential provider in the sign\-in UI process. When a user successfully signs in with a smart card, the smart card credential provider captures the reader name. This information is then stored in the registry with the session identifier where the sign in was initiated.

2.  The smart card resource manager service notifies the smart card removal policy service that a sign\-in has occurred.

3.  ScPolicySvc retrieves the smart card information that the smart card credential provider stored in the registry. This call is redirected if the user is in a remote session. If the smart card is removed, ScPolicySvc is notified.

4.  ScPolicySvc calls Remote Desktop Services to take the appropriate action if the request is to sign out the user or to disconnect the user's session, which might result in data loss. If the setting is configured to lock the computer when the smart card is removed, ScPolicySvc sends a message to Winlogon to lock the computer.

## See also
[How Smart Card Sign\-in Works in Windows](assetId:///36330874-3984-4551-ac31-cccd52fd3c92)

