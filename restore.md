# *Restore*

The Restore command takes data that has been stored in a target and copies it to a source.  It moves data in the reverse direction of of a Backup.
<p align="center">
<img src="images/restorecmd.png" width="394" height="102">
</p>

Restore ***from*** a target ***to*** a source.
 
The command can be constructed to restore the data back to the original volume or to a different volume.


# Syntax
The generic syntax of a Backup REST command, shown using curl is:

```
curl -X POST <ip>:<port>/v2/<tenant>/jobs/<export_job_id> 
     [-d '{"restore_type": <restore type>,
            "restore_id" : <restore id>}']
```

 - **ip**:	the IP address of the Snappy Frontend
 - **port**:	the listening port of the Snappy Frontned
 - **tenant**:	a valid tenant that has been set up in Snappy Frontend
 - **export_job_id**:  the job to restore (must be an "export" job)
 - **restore_type**:  The type of volume to restore to *(optional)*
 - **restore_id**:  The id of the volume to restore to *(optional)*

# Examples
Restore the volume as saved in job 123 to its original location:
```
curl -X POST 10.20.30.49:8080/v2/default/jobs/123  
```
Restore the volume saved in job 123 back to rbd volume “abcd-1234-efgh-5678”:
```
curl -X POST 10.20.30.49:8080/v2/default/jobs/123
     -d '{"restore_type": "rbd",
           "restore_id" : "abcd-1234-efgh-5678"}'
```
 
 

