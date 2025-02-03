# Kluge Quickstart Guide

##### Kubernetes-Linux Unified Grid Engine
![kluge-logo](https://github.com/user-attachments/assets/c7454790-38cc-459c-bfcc-8ee95006935f)


## What is Kluge?
Kluge is a Kubernetes-native batch processing system designed to be familiar for Slurm users while being accessible to newcomers. It converts simple, clean sbatch-style batch files into Kubernetes workloads seamlessly, using Volcano for scheduling. With a desktop-centric workflow, Kluge provides native status windows and delivers output directly to users' local machines, making job management seamless and intuitive.

---

## Step 1: Consult the CLI Reference
Kluge provides a built-in CLI reference to help you get started quickly. You can view available commands by running:

```bash
kluge batch --help
```

Here’s an example of the CLI help output:
<img width="1103" alt="Screenshot 2025-02-03 at 10 37 50 AM" src="https://github.com/user-attachments/assets/a93d4712-8ea7-4bad-88d8-8cc52334c23b" />

---

## Step 2: Create a Batch File
Kluge batch jobs are defined in a simple syntax. Below is an example batch file named `job.kb`:

```plaintext
JOB my_first_job
CPUS 2
MEM 4Gi
NODES 1
IMAGE python:3.9-slim

RUN {
  pip3 install --user pillow opencv-python-headless numpy
  python3 script.py
  echo "Job completed on $(hostname)"
}
```

This file defines:
- A job named `my_first_job`
- Requesting 2 CPUs and 4Gi of memory
- Running on 1 node
- Using a Python 3.9 slim container
- Running commands inside the container

---

## Step 3: Submit the Job
Once the batch file is ready, submit it using:

```bash
kluge batch job.kb
```

This will create a Kubernetes job via Volcano. You can check the status using:

```bash
kluge batch --watch my_first_job
```

---

## Step 3a: Optional Popup for Job Monitoring
If enabled, Kluge can show a more detailed job monitoring popup:

<img width="289" alt="Screenshot 2025-02-03 at 10 31 50 AM" src="https://github.com/user-attachments/assets/b46fc4ab-92ff-4a12-80f0-5f08d0bf1ad0" />

This view provides real-time CPU, memory usage, and node allocation.

<img width="712" alt="Screenshot 2025-02-03 at 10 31 56 AM" src="https://github.com/user-attachments/assets/eda43fda-f78d-4d76-8a11-b9d203bcb18f" />

---

## Step 4: Job Execution and Output Retrieval
Once the job completes, output files will be placed in the *user’s desktop* or other directory on their workstation. No shared ephemeral storage is needed in Kluge!

In the following screenshot, we create a job that ran a simple image manipulation script. The output for each host appears on the desktop.

<img width="836" alt="Screenshot 2025-02-03 at 10 58 53 AM" src="https://github.com/user-attachments/assets/8996a3be-75c2-4504-a423-ca01304c57f6" />

---

## Summary
1. Check CLI reference for syntax.
2. Create a batch file with job specs.
3. Submit the job via `kluge batch`.
4. Monitor execution via CLI or optional popup.
5. Retrieve output when the job completes.

Kluge simplifies batch processing on Kubernetes while keeping things intuitive and familiar!

For more details, check out the full documentation at [Kluge Docs](#).
