# Pre-compiled Ipopt MEX for MATLAB on macOS

This repository contains pre-compiled MEX files necessary to use the [Ipopt](https://github.com/coin-or/Ipopt) optimization solver in MATLAB on modern macOS (Apple Silicon).

The primary goal is to avoid recompiling the MEX interface on every new machine. The files included are:
*   `ipopt.mexmaca64`: The main compiled interface.

## Setup Instructions

Follow these steps to get Ipopt running in MATLAB on a new Mac.

### Step 1: Install Ipopt Library via Homebrew

The MEX file is only an *interface* to the main Ipopt library. You must have the library installed. The easiest way is with [Homebrew](https://brew.sh/).

In your Terminal, run:
```bash
brew install ipopt
```

### Step 2: Create a Central MATLAB Add-ons Folder

It is best practice to keep third-party toolboxes in a dedicated folder. If you don't have one already, create one in your Documents folder.

```bash
# This command creates the directory if it doesn't already exist
mkdir -p ~/Documents/MATLAB_Addons
```

Now, copy the two files from this repository (`ipopt.mexmaca64` and `ipopt_auxdata.m`) into this new folder.

### Step 3: Remove macOS "Quarantine" Attribute

When you download files from the internet (including via `git clone`), macOS adds a security attribute that prevents them from running. You must manually remove this attribute to allow MATLAB to use the MEX file.

1.  Navigate to your add-ons folder in the Terminal:
    ```bash
    cd ~/Documents/MATLAB_Addons
    ```
2.  Run the `xattr` command to remove the quarantine flag from the MEX file:
    ```bash
    xattr -d com.apple.quarantine ipopt.mexmaca64
    ```
    > **Note:** You only need to do this once on each new machine after downloading the files.

### Step 4: Add the Folder to the MATLAB Path

Finally, tell MATLAB where to find the Ipopt files.

1.  Open MATLAB.
2.  In the MATLAB Command Window, run the `pathtool` command:
    ```matlab
    >> pathtool
    ```
3.  In the "Set Path" window that opens, click **"Add Folder..."**.
4.  Navigate to and select the `MATLAB_Addons` folder (`Documents/MATLAB_Addons`).
5.  Click **"Save"** to make this change permanent.
6.  Click **"Close"**.

### Step 5: Verify the Installation

You're all set! To confirm that MATLAB can find Ipopt, run the `which` command:

```matlab
>> which ipopt
```

MATLAB should respond with the path to the file, confirming it is ready to use:
```
>> /Users/yourusername/Documents/MATLAB_Addons/ipopt.mexmaca64
```
