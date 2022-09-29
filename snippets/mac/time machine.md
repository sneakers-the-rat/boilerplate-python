[[Backup]]s of [[macOS]]
## See Time Machine logs
```bash
printf '\e[3J' && log show --predicate 'subsystem == "com.apple.TimeMachine"' --info --last 6h | grep -F 'eMac' | grep -Fv 'etat' | awk -F']' '{print substr($0,1,19), $NF}' 
```

## [[tmutil]]
https://ss64.com/osx/tmutil.htmlhttps://ss64.com/osx/tmutil.html

seems to be the main way to admin

https://krypted.com/mac-os-x/ins-outs-using-tmutil-backup-restore-review-time-machine-backups/

