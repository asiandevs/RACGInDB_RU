# RACGInDB_RU
Oracle RAC Grid Infrastructure and Oracle Home patch - RU January'19 
RU 18.3 to 18.5 

# Release Update for RAC GI and Oracle_HOME

# Variables
```
---

oracle_user:                     "oracle"
oracle_install_group:            "oinstall"
patch_dir:                       "/u01/patches"
patchid:                         "28828717"
tmp_dir:                         "/u01/app/temp"
logdir:                          "/tmp/{{ patchid }}"
oracle_home:                     "/u02/app/oracle/product/18.3.0/dbhome_1"
grid_home:                       "/u02/app/18.3.0/grid"
stage_dir:                       "/u01/stage"
root_user:                       "root"
grid_user:                       "grid"
date:                            "{{ lookup('pipe', 'date +%Y%m%d-%H%M') }}"
```

Tree Structure for this role is -

```
[root@oel75 ansible]# tree roles/racdb_patch_apply/
roles/racdb_patch_apply/
├── defaults
│   └── main.yml
├── files
│   └── sqlpatch.sql
├── tasks
│   ├── main.yml
│   ├── postpatch_apply.yml
│   └── prepatch_apply.yml
├── templates
└── vars
    └── main.yml

5 directories, 6 files
```

Tasks:
main.yml 

## Prepatch
```
 - pre_tasks_before_apply [prepatch_apply.yml]
     +  Backup opatch file from grid home / oracle home
	 +  Update required opatch utility in grid home / Oracle home
	 +  Update opatch ownership in grid home / Oracle home
	 +  OPatch Conflict Check in grid home / Oracle home
	 +  OPatch SystemSpace Check in grid home / Oracle home
	 +  check inventory for grid home / Oracle home
	 +  One-Off Patch Conflict Detection (-analyze)
	 +  current patch information
```
## Patch Nodes
```
 - RU to grid home first node
 - RU to grid home second node
 - Pause after GI patching completion
 - RU to database home first node
 - RU to database home second node 
 ```
 ## PostPatch
 ```
 - post_tasks_after_apply [postpatch_apply.yml]
     + Apply data patch
```
