---
layout: Share
title: Check Remote Server
parent: Checks
version: 1
date: 2020-07-03
tested_on: 3.x
---

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
