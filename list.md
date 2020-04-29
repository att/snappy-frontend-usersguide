
  
# *List*

The List command shows jobs that are in the Snappy Database.  This includes past jobs, current jobs and jobs that are scheduled to run in the future.  
 
The command can be constructed to show a summary or full detail, one or all jobs, and output as JSON or in a human readable format.


# Syntax
The generic syntax of a List REST command, shown using curl is:

```
curl –X GET <ip>:<port>/v2/<tenant>/jobs/<summary|full>[/<job_id>][.txt]
```

 - **ip**:	the IP address of the Snappy Frontend
 - **port**:	the listening port of the Snappy Frontned
 - **tenant**:	a valid tenant that has been set up in Snappy Frontend
 - **summary | full**: option to show all of the information about a job, or just a summary
 - **job_id**:  for specific jobs queries, which job to return information on
 - **.txt**:  change output from JSON (default) to human readable

# Examples
Summary of all jobs:
```
curl –X GET 10.20.30.41:8080/v2/default/jobs/summary  
```
Full description of all jobs:
```
curl –X GET 10.20.30.41:8080/v2/default/jobs/full
```
 
Summary of job 123:
```
curl –X GET 10.20.30.41:8080/v2/default/jobs/summary/123  
```
Full details of job 123:
```
curl –X GET 10.20.30.41:8080/v2/default/jobs/full/123  
```

These will result in the output being in JSON.  To show the output in human readable format, append **.txt** to any command.

# Output Examples
 Summary output, all jobs (human readable)
```
curl –X GET 127.0.0.1:8888/v2/default/jobs/summary
```
```
id  state  done  result  feid     arg0             arg1
1   Done    1      0     rbdtest  bk_single_sched  { "full_bk_intvl" : 2, "incr_bk_intvl" : 3, "count": 1, "sched_time": 0 }
2   Done    1      0     rbdtest  bk_single_full
3   Done    1      0     rbdtest  snap
4   Done    1      0     rbdtest  export
5   Done    1      0     rbdtest  put
6   Done    1      0     rbdtest  rstr_single      {"rstr_to_job_id" : 4}
7   Done    1      0     rbdtest  get              {"rstr_to_job_id" : 4}
8   Done    1      0     rbdtest  import
```
<br><br>

Single job output (JSON)
```
curl -X GET http://127.0.0.1:8888/v2/default/jobs/full/5
```
```
{"log": "[[4,\"export\",0,1,1586919757,0,{}],[5,\"put\",1,8,1586919757,0,{}],[5,\"put\",8,32,1586919758,0,{}],[5,\"put\",32,2,1586919759,0,{}]]", "feid": "rbdtest", "parent": 4, "grp": 3, "arg0": "put", "arg1": "", "arg2": "{\"sp_id\":\"0\",\"sp_name\":\"rbd\",\"sp_param\":{\"alloc_size\":12272640,\"image\":\"rbdtest\",\"key\":\"AQCCeJZeqIKDGhAAq4lUQRO2N0GoU3Y/Fi2PHA==\",\"mon_host\":\"127.0.0.1\",\"pool\":\"rbd\",\"snap_fin\":1586919754,\"snap_name\":\"snpy-3\",\"snap_start\":1586919754,\"user\":\"admin\",\"vol_size\":104857600},\"sp_ver\":\"0.1.0\",\"tp_id\":\"1001\",\"tp_name\":\"s3\",\"tp_param\":{\"container\":\"snappybackups\",\"password\":\"password\",\"put_fin\":1586919758,\"put_start\":1586919757,\"region\":\"default\",\"url\":\"127.0.0.1:38000\",\"user\":\"snappy\"},\"tp_ver\":\"0.1.0\"}", "arg3": "", "arg4": "", "arg5": "", "arg6": "", "next": 0, "state": 2, "done": 1, "result": 0, "policy": 5, "arg7": "", "root": 0, "id": 5, "sub": 0}
```
