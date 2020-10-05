---
title: Memory leak in remote registry service
description: Describes a memory leak issue that causes Windows Server 2012 and Windows 8 to hang. This memory leak involves the WnF tag, which consumes all available paged pool memory. A workaround is provided.
ms.date: 09/17/2020
author: Deland-Han 
ms.author: delhan
manager: dscontentpm
audience: itpro
ms.topic: troubleshooting
ms.prod: windows-client
localization_priority: medium
ms.reviewer: kaushika
ms.prod-support-area-path: Slow Performance
ms.technology: Performance
---
# Memory leak in the remote registry service causes Windows to hang

This article provides a solution to a memory leak issue in the remote registry service that causes Windows Server 2012 and Windows 8 to hang.

_Original product version:_ &nbsp; Windows 10 - all editions, Windows Server 2012 R2  
_Original KB number:_ &nbsp; 3105719

## Symptoms

On a Windows-based computer, you notice that more system memory and paged pool memory are being consumed than expected. This memory leak occurs after about 10 minutes of system uptime and eventually causes the system to hang.

Additionally, PoolMon analysis may show that the Windows Notification Facility (WnF) tag is consuming all the available paged pool memory.

## Cause

The issue occurs in the Endpoint Mapper Logic component. The Remote Registry service is designed to stop running after the connection has been idle for 10 minutes.

## Workaround

To work around this issue, follow these steps:

1. Open the run command box by pressing the Windows key+R.
2. Type regedit.exe, and then press Enter.
3. Locate the following registry subkey:

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\RemoteRegistry` 
4. In the details pane (on the right side), double-click DisableIdleStop.
5. Change the value to 00000001.

    > [!NOTE]
    > The default value is 00000000.

6. Exit Registry Editor.

For more information on Poolmon.exe, see the following Knowledge Base article:

[177415](https://support.microsoft.com/help/177415)  How to use Memory Pool Monitor (Poolmon.exe) to troubleshoot kernel mode memory leaks