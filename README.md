# Windows Notes

## Robocopy
After looking around on the web and trying to use robocopy, this is what works best for me... 

Robocopy to make backups:
```
                       everything (why no /MIR - DONT want /PURGE if you mess up dir names.... , even empty dirs)
                       .  verbose 
                       .  .  exclude system files
                       .  .  .      exclude app datea files
                       .  .  .      .           exclude juctions 
                       .  .  .      .           .    retry on error     
                       .  .  .      .           .    .    wait 15 seconds on error 
                       .  .  .      .           .    .    .     no progress (% does not look good in logfiles )
                       .  .  .      .           .    .    .     .   logfile (always append to logfile)
    robocopy $SRC $DES /E /V /XA:SH /XD AppData /XJD /R:5 /W:15 /NP /LOG+:Backup.log
```    

Scan Skipped files from robocopy log
```
find /v "New File" Backup.log | find /v "New Dir"
```

Tail ( watch the file as it progresses ( powershell )
```
Get-Content .\Backup.log -Tail 1 -Wait
```
