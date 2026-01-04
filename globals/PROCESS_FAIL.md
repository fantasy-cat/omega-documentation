# PROCESS_FAIL

This is used for the `on_process_fail` callback.

| Code                          | Meaning/Trigger                                                                                                    |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------|
| PROCESS_FAIL_CODE_SET_PROCESS | If `process:set` fails, or Omega fails to gain access to a process for whatever reason, this is triggered.         |
| PROCESS_FAIL_CODE_GET_MODULE  | If `process:get_module` fails, or Omega fails to gain access to the module for whatever reason, this is triggered. |
| PROCESS_FAIL_CODE_CALIBRATION | If `fantasy.calibrate` fails (which is usually only called from `constellation.lua`), then this is triggered.      |
| PROCESS_FAIL_CODE_MONITOR     | If `process:monitor` fails for whatever reason, or the process may have been closed, this is triggered.            |
| PROCESS_FAIL_CODE_SCRIPT_LOAD | If a script failed to load for whatever reason (even script errors), this is triggered.                            |
