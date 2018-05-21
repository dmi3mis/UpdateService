# UpdateService
Update windows servers without service downtime


# SYNTAX
Update-Servers.ps1 [[-ServerList] <String[]>] [[-ServerListFile] <String>] [[-SkipServers] <String[]>]
[[-SMTPServer] <String>] [[-SMTPFrom] <String>] [[-SMTPTo] <String>] [-NoPostStep] [-OnlyCheckReboot] 
[-OnlyPostStep] [-OnlyShowList] [-DontStopOnError]
    
  - ServerList - comma separated list of servers to update. Can be mask: for example exch-srv*
  - ServerListFile - file with servers list to update (one per line)<br/>
  *If ServerList parameter is defined this list will be added, if no of list parameters is defined, list will be getted from Active Directory*
  - SkipServers - comma separated list skipped servers. Can be mask: for example exch-srv*
  - SMTPServer - ip address or fqdn of smtp server, used to send reports. Currently supports only anonymous smtp
  - SMTPFrom - <from> field in report letters
  - SMTPTo - comma separated list of report letters resipients
  - NoPostStep - don't exit maintenance mode
  - OnlyPostStep - perform only post steps (exit maintenance mode)
  - OnlyCheckReboot - check for reboot pending and reboot server with enter/exit maintenance mode
  - OnlyShowList - only shows generated list of servers to update
  - DontStopOnError - don't stop execution if any error occured. By default script execution will stop

# Update process

Update process flow for one server shown in UpdateProcess.png

 - First, update script uses *_Helpers\Get-InstalledFeatures.ps1*_ for get server roles. This script returns array of server roles names (feel free to add nedeed roles detection"
 - Script check for available updates for server
 - - if updates not available, go to next server processing
 - - if updates available
 - - - Enter maintenance mode, by execution scripts from *Pre* folder - scripts selected by names, contains in server roles list
 - - - Check for server pending reboot. Reboot if necessary
 - - - Check and install updates. Check for pending reboot. Reboot if necessary. Loop until no updates is available
 - - - Exit maintenance mode, by execution scripts from *Post* folder - scripts selected by names, contains in server roles list
 
 # Existing maintenace modules
 
 # Config format
 
 # Maintenance module description
 
 # Coming soon
 
 Script for creation update powershell session on servers
