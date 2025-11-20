# Install Python Core/win32api


The Python Core / win32api module is used to interact with the Windows system and
is required for advanced features such as handling virtual machines with commands and
using things from your computer in your virtual machines

<section>
- Refer [How to Fix Missing Dependencies Python Core / win32api in VirtualBox](https://www.sysnettechsolutions.com/en/fix-python-win32api-virtualbox/)
- Download and install python from https://www.python.org/downloads/
- Now, open PowerShell/CMD as admin, and type 
    ```
    py -m pip install pywin32
    ```
- If you see a new Pip update, run the command below to update it quickly 
    ```
    python.exe -m pip install --upgrade pip
    ```
- Run the pip install for pywin32 again
</section>