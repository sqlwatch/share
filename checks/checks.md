---
title: Checks
has_children: true
permalink: /checks/
---

## Checks

Checks are defined in the `[dbo].[sqlwatch_config_check]` table. 
Code samples in this section must comply with the `check_query` requirement to always return a single numerical value in the `@output` variable. 
Thresholds can be set per individual requirements.

For example, a check for CPU utilisation, will always return the `@output` variable which will be compared to the set thresholds.

```
select @output=avg(pc.cntr_value_calculated)
from [dbo].[sqlwatch_logger_perf_os_performance_counters] pc
inner join [dbo].[sqlwatch_meta_performance_counter] mpc
	on pc.sql_instance = mpc.sql_instance
	and pc.performance_counter_id = mpc.performance_counter_id
where mpc.sql_instance = @@SERVERNAME
  and object_name = 'win32_perfformatteddata_perfos_processor'
  and counter_name = 'Processor Time %'
and snapshot_time > '{LAST_CHECK_DATE}'
```

To raise Warning when the CPU utilisation is above 60%, we will set the treshold to `[check_threshold_warning] = '>60'`. And to raise an Error (Critical) when it reaches 80%, we can set the critical treshold to: `[check_threshold_critical] = '>80'`
