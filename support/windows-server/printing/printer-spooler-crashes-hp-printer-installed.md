---
title: The printer spooler may crash randomly on a Windows Server computer that has an HP printer installed
description: Describes a problem in which the printer spooler may crash randomly on a Windows Server computer that has an HP printer installed.
ms.date: 09/08/2020
author: Deland-Han
ms.author: Deland-Han
manager: dscontentpm
audience: itpro
ms.topic: troubleshooting
ms.prod: windows-server
localization_priority: medium
ms.reviewer: kaushika
ms.prod-support-area-path: Errors and troubleshooting - Print spooler
ms.technology: PrintFaxScan
---
# The printer spooler may crash randomly on a Windows Server computer that has an HP printer installed

This article discusses an issue in which the printer spooler crashes randomly on a Windows Server computer that has an HP printer installed.

_Original product version:_ &nbsp;Windows Server 2012 R2  
_Original KB number:_ &nbsp;947477

## Symptoms

On a Windows Server based computer that has an HP printer installed, the printer spooler may crash randomly.

## Cause

This problem occurs because of one of the following files:

- Hpbmmon.dll (HP Master Monitor)
- Hpzpi4wm.dll (HP Print Processor)
- Hpzpp4wm.dll (HP Print Processor)
- HPtcpMon.dll (HP TCP Port monitor)

## Resolution

To resolve this problem, contact the third-party manufacturer for help.

## Workaround

> [!IMPORTANT]
> This section, method, or task contains steps that tell you how to modify the registry. However, serious problems might occur if you modify the registry incorrectly. Therefore, make sure that you follow these steps carefully. For added protection, back up the registry before you modify it. Then, you can restore the registry if a problem occurs. For more information about how to back up and restore the registry, click the following article number to view the article in the Microsoft Knowledge Base: [322756](https://support.microsoft.com/help/322756) How to back up and restore the registry in Windows  

Workaround for the problem that is caused by the Hpbmmon.dll file 

To work around this problem, remove the HP Master Monitor. To do this, follow these steps:
1. Start Registry Editor.
2. Locate and then click the following registry subkey: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Print\Monitors\HP Master Monitor` 

3. On the **File** menu, click **Export**.
4. In the **File name** box, type HPprinter, and then click **Save**.

    > [!NOTE]
    > If you want to restore this registry subkey, double-click the HPprinter.reg file that you save in this step.
5. Right-click the **HP Master Monitor** registry entry, and then click **Delete**.
6. Click **Yes**.
7. Exit Registry Editor, and then restart the computer.
8. Rename the Hpbmmon.dll file to "Hpbmmon.old." The file is in the following location: C:\WINDOWS\system32\Hpbmmon.dll file

Workaround for the problem that is caused by the Hpzpi4wm.dll file or the Hpzpp4wm.dll file 

> [!NOTE]
> If this printer does not work with WinPrint, the following steps may not work. If this situation occurs, contact HP to upgrade the HPZPP4WM print processor to the newer version.

1. Click **Start**, and then click **Control Panel**.
2. Double-click **Printers and Faxes**.
3. Right-click the printer that you want to use, and then click **Properties**.
4. Click the **Advanced** tab, and then click **Print Processor**.
5. Click **WinPrint** in the **Print processor** box, click **RAW** in the **Default data type** box, and then click **OK** two times.
6. Rename the Hpzpi4wm.dll file to "Hpzpi4wm.old." The file is in the following location: C:\WINDOWS\system32\spool\drivers\w32x86\3\Hpzpi4wm.dll

7. Rename the Hpzpp4wm.dll file to "Hpzpp4wm.old." The file is in the following location: C:\WINDOWS\system32\spool\PRTPROCS\W32X86\Hpzpp4wm.dll

Workaround for the problem that is caused by the HPtcpMon.dll file 
1. Start Registry Editor.
2. Locate and then click the following registry subkey: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Print\Monitors\HP Standard TCP/IP Port` 

3. On the **File** menu, click **Export**.
4. In the **File name** box, type HPprinter, and then click **Save**.

    > [!NOTE]
    > If you want to restore this registry subkey, double-click the HPprinter.reg file that you save in this step.
5. Right-click the **HP Standard TCP/IP Port** registry entry, and then click **Delete**.
6. Click **Yes**.
7. Locate and then click the following registry subkey: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Print\Monitors\Standard TCP/IP Port` 

8. Double-click **Driver**, and then verify that the value of the **Value data** box is **tcpmon.dll**.

    > [!NOTE]
    > If the Driver registry entry does not exist or its value is not tcpmon.dll, create the Driver registry entry, and then set its value to tcpmon.dll. To do this, follow these steps:
    1. On the **Edit** menu, point to **New**, and then click **String Value**.
    2. Type Driver, and then press ENTER.
    3. Right-click **Driver**, and then click **Modify**.
    4. In the **Value data** box, type tcpmon.dll, and then click **OK**.
9. Exit Registry Editor, and then restart the computer.
10. Rename the HPtcpMon.dll file to "HPtcpMon.old." The file is in the following location: C:\WINDOWS\system32\HPTcpMon.dll


## More information

The third-party products that this article discusses are manufactured by companies that are independent of Microsoft. Microsoft makes no warranty, implied or otherwise, about the performance or reliability of these products. 

For more information about how to troubleshoot printing problems in Windows 2000 and in Windows Server 2003, click the following article number to view the article in the Microsoft Knowledge Base:

[260142](https://support.microsoft.com/help/260142) How to troubleshoot printing problems in Windows 2000 and in Windows Server 2003