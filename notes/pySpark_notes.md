# PySpark Notes

## How to suppress Spark output in Jupyter notebooks  
1. In terminal, create a default profile:
```
ipython profile create
```
  - The command above will print out two file paths for the config files it generated.
  - **Copy the second path**, the one ending with ipython_kernel_config.py, and paste it in the command below.

2. Write to the kernel config file to turn off the capture flag:
```
echo "c.IPKernelApp.capture_fd_output = False" >> \
  "<REPLACE THIS WITH THE FILE PATH FOR ipython_kernel_config.py>"
```

Source: [this SO answer](https://stackoverflow.com/a/70613254/23800771)
