## Locations

- local: /media/valeriu/0a4de3db-bc01-4daa-a42c-2c16c2e081bc/RAMIP/MIROC/MIROC6/
- jasmin: /gws/nopw/j04/ramip/RAMIP/MIROC6

## Globus

JASMIN instructions:
- general Globus: <https://help.jasmin.ac.uk/docs/data-transfer/globus-command-line-interface/>
- Globus Personal API and GUI: <https://help.jasmin.ac.uk/docs/data-transfer/globus-connect-personal/> 

Environment file:

```
---
name: globus-env
channels:
  - conda-forge
  - nodefaults

dependencies:
  - globus-cli
```

Globus versioning:

```
(globus-env) valeriu@valeriu-PORTEGE-Z30-C:~$ conda list globus
# packages in environment at /home/valeriu/miniconda3/envs/globus-env:
#
# Name                     Version          Build            Channel
globus-cli                 3.39.0           pyhd8ed1ab_0     conda-forge
globus-sdk                 3.65.0           pyhd8ed1ab_0     conda-forge
```

- set up an identity, the run `globus login`
- set JASMIN default collection: `export jdc=a2f53b7f-1b4e-4dce-9b7c-349ae760fee0`
- first time, that will need JASMIN-Globus authorization: `globus session consent 'urn:globus:auth:scope:transfer.api.globus.org:all[*https://auth.globus.org/scopes/a2f53b7f-1b4e-4dce-9b7c-349ae760fee0/data_access]'`
- use regular UNIX ops now: `globus ls $jdc:/gws/nopw/j04/ramip/RAMIP/`
- get globus personal: see instructions for Globus Personal
- new endpoint is 5d7a0948-af42-11f0-b5e1-0affdd0cd947: `export pdc=5d7a0948-af42-11f0-b5e1-0affdd0cd947`
- source: $pdc:/media/valeriu/0a4de3db-bc01-4daa-a42c-2c16c2e081bc/RAMIP/MIROC/MIROC6/historical
- target: $jdc:/gws/nopw/j04/ramip/RAMIP/MIROC6
- start transferring:

```
globus transfer -r $pdc:/media/valeriu/0a4de3db-bc01-4daa-a42c-2c16c2e081bc/RAMIP/MIROC/MIROC6/historical $jdc:/gws/nopw/j04/ramip/RAMIP/MIROC6
```

which gets one:

```
$ globus transfer -r $pdc:/media/valeriu/0a4de3db-bc01-4daa-a42c-2c16c2e081bc/RAMIP/MIROC/MIROC6/historical $jdc:/gws/nopw/j04/ramip/RAMIP/MIROC6
Message: The transfer has been accepted and a task has been created and queued for execution
Task ID: 1beb8098-af45-11f0-9fba-027493648695
```

polling the task:

```
$ globus task show 1beb8098-af45-11f0-9fba-027493648695
Label:                        None
Task ID:                      1beb8098-af45-11f0-9fba-027493648695
Is Paused:                    False
Type:                         TRANSFER
Directories:                  3103
Files:                        1004
Status:                       ACTIVE
Request Time:                 2025-10-22T12:46:22+00:00
Faults:                       0
Total Subtasks:               4108
Subtasks Succeeded:           3104
Subtasks Pending:             1004
Subtasks Retrying:            0
Subtasks Failed:              0
Subtasks Canceled:            0
Subtasks Expired:             0
Subtasks with Skipped Errors: 0
Deadline:                     2025-10-23T12:46:22+00:00
Details:                      OK
Source Endpoint:              ramip
Source Endpoint ID:           5d7a0948-af42-11f0-b5e1-0affdd0cd947
Destination Endpoint:         JASMIN Default Collection
Destination Endpoint ID:      a2f53b7f-1b4e-4dce-9b7c-349ae760fee0
Bytes Transferred:            124470165504
Bytes Per Second:             105909886
```

## Transfer jobs

Web app: <https://app.globus.org/activity>

Incorrect DRS structure in `/gws/nopw/j04/ramip/RAMIP/MIROC6` (all historical exp ensembles dumped there).

- historical 1beb8098-af45-11f0-9fba-027493648695 8 jobs pending:
  - view job <https://app.globus.org/activity/1beb8098-af45-11f0-9fba-027493648695/overview>
  - jobs failed with FTP: permission denied
  - 996/1004 files correctly transferred = 5.15TB
  - effective speed: 57Mbps
  - all untransferred files are eSATA system files eg `RAMIP/MIROC/MIROC6/historical/r3i1p1f1/6hrPlev/pr/gn/v20250925/.nfs0000004c803581cf0000088b`

Correct DRS structure in `/gws/nopw/j04/ramip/RAMIP/MIROC6_V/`

- piClim-370           423c767c-affe-11f0-9d5e-027493648695 SUCCEEDED
- piClim-370-126aer    1cadefa2-b001-11f0-933f-0e092d85c59b SUCCEEDED
- piClim-370-afr126aer 8496e223-b003-11f0-acbb-027493648695 SUCCEEDED
- piClim-370-eas126aer dfa15443-b005-11f0-af56-0e092d85c59b SUCCEEDED
- piClim-370-nae126aer 53710b85-b008-11f0-af47-0e092d85c59b SUCCEEDED
- piClim-370-sas126aer ad4eb291-b00a-11f0-8a27-0e092d85c59b SUCCEEDED
- ssp370               d46fe836-b00d-11f0-bf4e-0e092d85c59b
- ssp370-126aer        31ca05bd-b015-11f0-a7c4-027493648695
- ssp370-afr126aer     6b805759-b015-11f0-8311-0affdd0cd947

## Unfinished transfers final logs

- historical (23 October 2025, 1200H):
```
(globus-env) valeriu@valeriu-PORTEGE-Z30-C:~$ globus task show 1beb8098-af45-11f0-9fba-027493648695
Label:                        None
Task ID:                      1beb8098-af45-11f0-9fba-027493648695
Is Paused:                    False
Type:                         TRANSFER
Directories:                  3103
Files:                        1004
Status:                       ACTIVE
Request Time:                 2025-10-22T12:46:22+00:00
Faults:                       63
Total Subtasks:               4108
Subtasks Succeeded:           4100
Subtasks Pending:             8
Subtasks Retrying:            0
Subtasks Failed:              0
Subtasks Canceled:            0
Subtasks Expired:             0
Subtasks with Skipped Errors: 0
Deadline:                     2025-10-26T06:30:12+00:00
Details:                      PERMISSION_DENIED
Source Endpoint:              ramip
Source Endpoint ID:           5d7a0948-af42-11f0-b5e1-0affdd0cd947
Destination Endpoint:         JASMIN Default Collection
Destination Endpoint ID:      a2f53b7f-1b4e-4dce-9b7c-349ae760fee0
Bytes Transferred:            5150263808476
Bytes Per Second:             64541290
```
