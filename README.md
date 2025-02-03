# Kluge Quickstart Guide

## What is Kluge?
Kluge is a Kubernetes-native batch processing system that translates familiar `sbatch`-style job submissions into Kubernetes workloads, specifically leveraging Volcano for scheduling. This allows users to easily run compute-heavy batch jobs on Kubernetes while maintaining a familiar workflow.

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

![Screenshot 2025-02-03 at 10.31.50 AM](/Users/simian/Desktop/Screenshots/Screenshot 2025-02-03 at 10.31.50 AM.png)

![Screenshot 2025-02-03 at 10.31.56 AM](/Users/simian/Desktop/Screenshots/Screenshot 2025-02-03 at 10.31.56 AM.png)

This view provides real-time CPU, memory usage, and node allocation.

---

## Step 4: Job Execution and Output Retrieval
Once the job completes, output files will be placed in the *user’s desktop* or other directory on their workstation. No shared ephemeral storage is needed in Kluge!

In the following screenshot, we create a job that ran a simple image manipulation script. The output for each host appears on the desktop.

![Screenshot 2025-02-03 at 10.58.53 AM](/Users/simian/Desktop/Screenshots/Screenshot 2025-02-03 at 10.58.53 AM.png)

---

## Summary
1. Check CLI reference for syntax.
2. Create a batch file with job specs.
3. Submit the job via `kluge batch`.
4. Monitor execution via CLI or optional popup.
5. Retrieve output when the job completes.

Kluge simplifies batch processing on Kubernetes while keeping things intuitive and familiar!

For more details, check out the full documentation at [Kluge Docs](#).
