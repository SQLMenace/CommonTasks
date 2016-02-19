
You can leave out | Out-GridView if you don't want the gridview output

```Powershell
gci . r -Path 'C:\Junkdraw' | sort Length -desc |
  Select-Object -Property FullName,
  @{Name='SizeGB';Expression={$_.Length / 1GB}} ,
  @{Name='SizeMB';Expression={$_.Length / 1MB}} ,
  @{Name='SizeKB';Expression={$_.Length / 1KB}} -f 10 | Out-GridView
```
