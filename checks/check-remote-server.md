---
parent: Checks
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
