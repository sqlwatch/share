---
layout: share
title: Check Remote Server
parent: Checks
version: 1.0
date: 2020-07-03
tested_on: 3.x
---

Check remote server availability using `sp_testlinkedserver`. As long as the remote server is online, the check will return 1. Set the threshold to alert when the `@output` is not 1: `[check_threshold_critical] = <>'1'`

```sql
BEGIN TRY
  EXEC master.sys.sp_executesql N'EXEC sp_testlinkedserver N''SQLWATCH-TEST-1'';';
  SELECT @output = 1
END TRY
BEGIN CATCH
  SELECT @output = 0
END CATCH

SELECT @output
```
