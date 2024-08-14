Example to run a python script `testbatch.py`

Make an shell file, eg `test.sh` containing:
```shell
#!/bin/bash
cd /vols/cms/lcr119/examples
python testbatch.py
```
then run `chmod u+x test.sh` to make it executable

>[!info]
>This is the executable that will be sent to HTCondor

You then need to create a submission file `test.sub`, for example:
```shell
executable = test.sh
output = ./test.$(ClusterId).$(ProcId).out
error = ./test.$(ClusterId).$(ProcId).err
log = ./test.$(ClusterId).log
should_transfer_files   = YES
when_to_transfer_output = ON_EXIT
+MaxRuntime = 6500
queue
```

>[!important]
>This .sub file is what you need to submit to the batch

eg: 
```shell
condor_submit test.sub
```

For a large amount of submissions, an example script is given here [[Bulk Submissions]]...




