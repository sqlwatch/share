---
layout: share
title: SQLWATCH_Performance_Counters_CL
parent: Reports
version: 1.0
date: 2020-07-05
tested_on: 3.x
---

Report query to send Performance Counters to Azure Log monitor

```
select 
	  d.[sql_instance]
	, m.[counter_name]
	, d.[instance_name]
	, h.report_time
	, d.[cntr_value_calculated]
	, h.snapshot_time_utc_offset
from [dbo].[sqlwatch_logger_perf_os_performance_counters] d
  	
inner join dbo.sqlwatch_logger_snapshot_header h
	on  h.snapshot_time = d.[snapshot_time]
	and h.snapshot_type_id = d.snapshot_type_id
	and h.sql_instance = d.sql_instance

inner join [dbo].[sqlwatch_meta_performance_counter] m
	on m.sql_instance = d.sql_instance
	and m.performance_counter_id = d.performance_counter_id

inner join [dbo].[sqlwatch_config_sql_instance] s
	on s.sql_instance = d.sql_instance

where h.snapshot_time > '{REPORT_LAST_RUN_DATE}'
and h.snapshot_time <= '{REPORT_CURRENT_RUN_DATE_UTC}'
and m.cntr_type <> 1073939712
```
