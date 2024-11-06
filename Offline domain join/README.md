# Windows Server: Offline domain join

<b>Documentation:</b>

[djoin](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/ff793312(v=ws.11))

<b>Notes:</b>

* Offline domain can be performed without connection to AD but connections is still required for first logon

<b>Create offline domain join files:</b>

```batch
djoin /provision /domain "ad.letsdoautomation.com" /machine "PC01" /savefile "C:\Users\%username%\Desktop\djoin\PC01.txt"
```

<b>Create offline domain join file with specific OU:</b>

```batch
djoin /provision /domain "ad.letsdoautomation.com" /machine "PC02" /machineou "OU=NewComputers,DC=ad,DC=letsdoautomation,DC=com" /savefile "C:\Users\%username%\Desktop\djoin\PC02.txt"
```

<b>Create multiple offline domain join files:</b>

```powershell
$computers =
"NB01",
"NB02",
"NB03",
"NB04",
"NB05",
"NB06",
"NB07",
"NB08",
"NB10"

foreach($computer in $computers){
    djoin /provision /domain "ad.letsdoautomation.com" /machine $computer /machineou "OU=NewComputers,DC=ad,DC=letsdoautomation,DC=com" /savefile "C:\Users\$($env:USERNAME)\Desktop\djoin\$($computer).txt"
}
```

<b>Perform offline join:</b>

```batch
djoin /requestodj /loadfile "C:\Users\admin\Desktop\NB05.txt" /windowspath C:\windows /localos
```