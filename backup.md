
  
# *Backup*

The Backup command takes data in a source and copies it to a target.  The data can be images, files, directories or anything else that has a plug-in.
<p align="center">
<img src="images/backupcmd.png" width="388" height="100">
</p>
 
Backup ***from*** a source ***to*** a target.
 
The command can can back up data directly from a source such as RBD (a "native" source for Snappy), or from a source that backed by a native source (Cinder backed by RBD).  In the second case, a Snappy Agent is used to translate the IDs between those two protocols.


# Syntax
The generic syntax of a Backup REST command, shown using curl is:

```
curl -X POST http://<ip>:<port>/v2/<tenant>/jobs/

[-H "Authorization:Basic <passcode>]
-d '{"source_type"  :"<volume_type>",
"source_id"  :"<volume_id>”,
"count"  :"<count>",
"full_interval" :"<interval_in_secs>",
"delta_interval":”<interval_in_secs>"}'
```

 - **ip**:	the IP address of the Snappy Frontend
 - **port**:	the listening port of the Snappy Frontned
 - **tenant**:	a valid tenant that has been set up in Snappy Frontend
 - **passcode**:  passcode for Basic authentication *(optional)*
 - **source_type**:  The type of volume to back up [rbd]
 - **source_id**:  The id of the volume to back up to 
 - **count**:  The total number of backups to perform
 - **full_interval**:  The number of *seconds* between full backups 
 - **delta_interval**:  The number of *seconds* between delta backups (not currently supported)

Regarding the *count* parameter, the first backup always starts immediately.

# Examples
A single backup will be submitted.  The  backup will start immediately.  RBD volume 9876-54321-AABBCC will be sent to the target defined by tenant "garnet".
```
curl -X POST http://192.168.1.201:8080/v2/garnet/jobs/
	-d '{"source_type"  :"rbd",
	       "source_id"  :"9876-54321-AABBCC",
	           "count”  :"1",
	    "full_interval” :"1"}'  
```
<br><br>
Daily backups (86400 seconds) will be submitted.  The first backup will start immediately and they will continue at the same time for the next 6 days, for the total of 7 backups.  The backups will be of Cinder ID ABCDEFGH-1234-5678-IJKLMNOPQRSTUVWX (or the storage type that is backing it) and will be send to the target defined by tenant "crimson", which requires Basic authentication.

```
curl -X POST http://192.168.1.201:8080/v2/crimson/jobs/
	-H "Authorization:Basic c25hcHB5Cg=="
	-d '{"source_type"  :"cinder_id",
	       "source_id"  :"ABCDEFGH-1234-5678-IJKLMNOPQRSTUVWX",
	           "count”  :"7",
	    "full_interval” :"86400"}'  
```
