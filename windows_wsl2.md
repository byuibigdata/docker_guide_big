# Docker a Windows Subsystem for Linux (WSL-2)

Windows 10 users will need to install [WSL-2](https://docs.microsoft.com/en-us/windows/wsl/install-win10). You can also find guidance from [Docker on the WSL-2 backend](https://docs.docker.com/docker-for-windows/wsl/) and a [blog post from Docker on the transition to WSL-2](https://www.docker.com/blog/docker-hearts-wsl-2/).  

## Memory settings

Based on [this guide](https://itnext.io/wsl2-tips-limit-cpu-memory-when-using-docker-c022535faf6f), you can do the following to manage the memory available to WSL-2.

1. Open Windows Terminal/CMD/PowerShell.

2. Run the following command.

    ```bash
    # turn off all wsl instances such as docker-desktop
    wsl --shutdown
    notepad "$env:USERPROFILE/.wslconfig"
    ```

3. Edit `.wslconfig` file with notepad and write down these settings:

    ```
    [wsl2]
    memory=5GB   # Limits VM memory in WSL 2 up to 5GB
    processors=4 # Makes the WSL 2 VM use two virtual processors
    ```

4. Save the `.wslconfig` file and restart Docker.

You can see the other [WSL 2 Settings](https://docs.microsoft.com/en-us/windows/wsl/wsl-config#wsl-2-settings) available for manipulation using the `.wslconig`.

### Other references

- [How to set up Docker within Windows System for Linux (WSL2) on Windows 10](https://www.hanselman.com/blog/how-to-set-up-docker-within-windows-system-for-linux-wsl2-on-windows-10)
- [VSCode: Docker in WSL2](https://code.visualstudio.com/blogs/2020/03/02/docker-in-wsl2)