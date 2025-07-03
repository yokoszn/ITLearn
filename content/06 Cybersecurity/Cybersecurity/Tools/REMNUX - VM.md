___
**Tags:** [[Defensive Security Tooling]] [[TryHackMe]][[Network Operations]] [[Digital Forensics]]
#hacking #certification-prep #Learning 

**Links:** 

---

One of the most common investigative practices in Digital Forensics is the preprocessing of evidence. This involves running tools and saving the results in text or JSON format. The analyst often relies on tools such as Volatility when dealing with memory images as evidence. This tool is already included in the REMnux VM. Volatility commands are executed to identify and extract specific artefacts from memory images, and the resulting output can be saved to text files for further examination. Similarly, we can run a script involving the tool's different parameters to preprocess the acquired evidence faster.  

  

### Preprocessing With Volatility

In this task, we will use the Volatility 3 tool version. However, we won’t go deep into the investigation and analysis part of the result—we could write a whole book about it! Instead, we want you to be familiar with and get a feel for how the tool works. Run the command as instructed and wait for the result to show. Each plugin takes 2-3 minutes to show the output.

Here are some of the parameters or plugins we will use. We will focus on Windows plugins.

- windows.pstree.PsTree
- windows.pslist.PsList
- windows.cmdline.CmdLine
- windows.filescan.FileScan
- windows.dlllist.DllList
- windows.malfind.Malfind
- windows.psscan.PsScan

Let’s get started then!

In your RemnuxVM, run `sudo su`, then navigate to **/home/ubuntu/Desktop/tasks/Wcry_memory_image/** directory, and our file would be **wcry.mem**. We will run each plugin after the command `vol3 -f wcry.mem`.

  

### PsTree

This plugin lists processes in a tree based on their parent process ID.

Terminal

```powershell
root@10.10.124.188:/home/ubuntu/Desktop/tasks/Wcry_memory_image$ vol3 -f wcry.mem windows.pstree.PsTree
Volatility 3 Framework 2.0.0
Progress:  100.00		PDB scanning finished
```

**View Results**
          

### PsList

This plugin is used to list all currently active processes in the machine.

Terminal

```powershell
root@10.10.124.188:/home/ubuntu/Desktop/tasks/Wcry_memory_image$ vol3 -f wcry.mem windows.pslist.PsList
Volatility 3 Framework 2.0.0
Progress:  100.00		PDB scanning finished
```

**View Results**
          

### CmdLine

This plugin is used to list process command line arguments.

Terminal

```powershell
root@10.10.124.188:/home/ubuntu/Desktop/tasks/Wcry_memory_image$ vol3 -f wcry.mem windows.cmdline.CmdLine
Volatility 3 Framework 2.0.0
Progress:  100.00		PDB scanning finished
```

**View Results**
          

### FileScan

This plugin scans for file objects in a particular Windows memory image. The results have more than 1,400 lines.

Terminal

```powershell
root@10.10.124.188:/home/ubuntu/Desktop/tasks/Wcry_memory_image$ vol3 -f wcry.mem windows.filescan.FileScan
Volatility 3 Framework 2.0.0
Progress:  100.00		PDB scanning finished
```

**View Results**
          

### DllList

This plugin lists the loaded modules in a particular Windows memory image. Due to a text limitation, this one won't have a View Results icon.

Terminal

```powershell
root@10.10.124.188:/home/ubuntu/Desktop/tasks/Wcry_memory_image$ vol3 -f wcry.mem windows.dlllist.DllList
Volatility 3 Framework 2.0.0
Progress:  100.00		PDB scanning finished
```

  

### PsScan

This plugin is used to scan for processes present in a particular Windows memory image.

Terminal

```powershell
root@10.10.124.188:/home/ubuntu/Desktop/tasks/Wcry_memory_image$ vol3 -f wcry.mem windows.psscan.PsScan
Volatility 3 Framework 2.0.0
Progress:  100.00		PDB scanning finished
```

**View Results**
          

### Malfind

This plugin is used to lists process memory ranges that potentially contain injected code. There won't be any View Results icon for this one due to text limitation.

Terminal

```powershell
root@10.10.124.188:/home/ubuntu/Desktop/tasks/Wcry_memory_image$ vol3 -f wcry.mem windows.malfind.Malfind
Volatility 3 Framework 2.0.0
Progress:  100.00		PDB scanning finished
```

  

For more information regarding other plugins, you may check this [link](https://volatility3.readthedocs.io/en/stable/volatility3.plugins.html).

Now, you have the plugins running individually and seeing the result. What you will do now is process this in bulk. Remember, one of the investigative practices involves preprocessing evidence and saving the results to text files, right? The question is how?

The answer? Do a loop statement! See the command below.

Terminal

```powershell
root@10.10.124.188:/home/ubuntu/Desktop/tasks/Wcry_memory_image$ for plugin in windows.malfind.Malfind windows.psscan.PsScan windows.pstree.PsTree windows.pslist.PsList windows.cmdline.CmdLine windows.filescan.FileScan windows.dlllist.DllList; do vol3 -q -f wcry.mem $plugin > wcry.$plugin.txt; done
```

Let’s break this command down, shall we?

- We created a variable named `$plugin` with values of each volatility plugin
- Then ran vol3 parameters `-q`, which means quiet mode or does not show the progress in the terminal
- And `-f,` which means read from the memory capture.
- The `plugin > wcry.plugin.done;` means run volatility with the plugins and output it to a file with wcry at the beginning of the text, followed by the name of the plugins and with an extension of `.txt`. Repeat until the value of variable $plugin is used.

After running the command, you won't see any output from the terminal; you'll see files within the same directory where you ran the command.

![This image shows the desired output of running the command from the instructions. You should be able to see seven text files generated from running the loop statement](https://tryhackme-images.s3.amazonaws.com/user-uploads/5e6bbe59a46ee9407fd65bbe/room-content/5e6bbe59a46ee9407fd65bbe-1727001460357.png)

  

### Preprocessing With Strings

Next, we will preprocess the memory image with the Linux strings utility. We will extract the **ASCII**, 16-bit **little-endian**, and 16-bit **big-endian** strings. See the command below.

Terminal

```powershell
root@10.10.124.188:/home/ubuntu/Desktop/tasks/Wcry_memory_image$ strings wcry.mem > wcry.strings.ascii.txt
root@10.10.124.188:/home/ubuntu/Desktop/tasks/Wcry_memory_image$ strings -e l  wcry.mem > wcry.strings.unicode_little_endian.txt
root@10.10.124.188:/home/ubuntu/Desktop/tasks/Wcry_memory_image$ strings -e b  wcry.mem > wcry.strings.unicode_big_endian.txt
```

The strings command extracts printable ASCII text. The `-e l` option tells strings to extract 16-bit little endian strings. The `-e b` option tells strings to extract 16-bit big endian strings. All three string formats can provide useful information about the system under investigation.

You should have the same output below.

![This image shows the desired output when you run the command as per instructions. You should have at least three text files generated from running the command.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5e6bbe59a46ee9407fd65bbe/room-content/5e6bbe59a46ee9407fd65bbe-1727002235999.png)

Now, this is ready for analysis, but remember, our goal here in this task is to preprocess the evidence so that any analyst who will investigate this can expedite searches and analysis.win