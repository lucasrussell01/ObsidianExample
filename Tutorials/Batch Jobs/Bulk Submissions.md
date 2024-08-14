You can automatically create submission and executable scripts and send them to the batch with something like this in python:

```python
import os

# Dummy script for automated job submission
def CreateSubmission(index):
    # create submission script
    file = open(f"job_{index}.sub", "w")
    file.write(f"executable = job_{index}.sh\n")
    file.write(f"output = ./job_{index}.$(ClusterId).$(ProcId).out\n")
    file.write(f"error = ./job_{index}.$(ClusterId).$(ProcId).err\n")
    file.write(f"log = ./job_{index}.$(ClusterId).$(ProcId).log\n")
    file.write("should_transfer_files   = YES\n")
    file.write("when_to_transfer_output = ON_EXIT\n")
    file.write("+MaxRuntime = 6500\n")
    file.write("queue\n")
    # add more lines as needed
    file.close()
    print(f"Created submission file [job_{index}.sub]")
    print(f"-----------------------------------------------------")
    return True

def CreateExecutable(index, argument):   
    # create the executable
    filename = f"job_{index}.sh"
    file = open(filename, "w")
    file.write("#!/bin/bash\n")
    file.write("cd /vols/cms/lcr119/examples\n")    
    file.write(f"python example_job.py --maxN={argument}\n") # arguments specified here
    file.close()
    # make executable
    os.system(f"chmod u+x {filename}")
    print(f"Created executable [{filename}] with parameter {argument} ")
    return True

def SubmitJob(index):
    # send the job to the batch    
    os.system(f"condor_submit job_{index}.sub")
    print(f"job_{index}.sub submitted :) \n")
    return True


param_to_vary = range(100, 110)

index = 0 # track job file name

for p in param_to_vary:
    CreateExecutable(index, p)
    CreateSubmission(index)
    SubmitJob(index)
    index += 1# change job index so don't overwrite
```