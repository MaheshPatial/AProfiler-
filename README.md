# AProfiler

<img src="https://github.com/MaheshPatial/Images/blob/master/Aprofiler1.png" width="180px"/>
<img src="https://github.com/MaheshPatial/Images/blob/master/Aprofiler2.png" width="180px" />


Aprofiler monitors and records the CPU and memory usage of Android devices.

## Details

Aprofiler shows the device CPU and memory status in real time.

It has two main options:
- It shows a chart and several labels wherein the values of the CPU and memory usage are updated every 0.5, 1, 2 or 4 seconds.
- It can record on a CSV file the read values for a later usage on a spreadsheet program.

When Aprofiler is running on the background it consumes little resources. Then it can monitor and record the CPU and memory usage of other applications on the foreground.

Aprofiler adds a *Record* and *Close* button to the Aprofiler entry on the notification drawer.

#### How CPU and memory usage are obtained

In order to get the CPU usage the app does NOT make use of the [`top`](https://en.wikipedia.org/wiki/Top_(software)) command from Linux but instead it parses `/proc/stat` and rest of process folders from the [`procfs`](https://en.wikipedia.org/wiki/Procfs) file system and work out the calculations with the user and system time. This is implemented on [`ServiceReader.class`]

https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk65143



#### Retrieving processes info since Android Oreo 8.0 (API 26, August 2017)

In Android 8.0 Google has further restricted access to the `proc` file system. Until now it was possible to at least get process info of the process running Aprofiler and total CPU usage. This does not work any more. Aprofiler running on devices with Android 8.0 will only show memory usage, but not total CPU usage or CPU usage for any process, including the own app process. Running the app on a rooted device does not make difference.


## Resolving dependencies

Aprofiler only has one external dependency, [AndroidProcesses](https://github.com/jaredrummler/AndroidProcesses). It is used to retrieve the device processes list and populate the 'Processes' screen.
