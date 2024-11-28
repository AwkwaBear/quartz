This guide is for setting up a Jupyter Notebook to run within VS Code using WSL (Windows Subsystem for Linux) Ubuntu and a Conda environment as a backend. This guide can be followed end to end to set up a new environment or using an existing cloned repo.

>[!SUMMARY] Table of Contents
>- [[Jupyter Notebooks using WSL and VScode setup guide#Install WSL via powershell|Install WSL via powershell]]
>- [[Jupyter Notebooks using WSL and VScode setup guide#Install and Setup WSL Ubuntu|Install and Setup WSL Ubuntu]]
>- [[Jupyter Notebooks using WSL and VScode setup guide#Install Miniconda in Ubuntu|Install Miniconda in Ubuntu]]
>    - [[Jupyter Notebooks using WSL and VScode setup guide#Setup Conda environment|Setup Conda environment]]
>- [[Jupyter Notebooks using WSL and VScode setup guide#VScode Setup|VScode Setup]]
>- [[Jupyter Notebooks using WSL and VScode setup guide#Connect to WSL using VSCode|Connect to WSL using VSCode]]
>- [[Jupyter Notebooks using WSL and VScode setup guide#Adding or Removing files from Ubuntu environment|Adding or Removing files from Ubuntu environment]]
>    - [[Jupyter Notebooks using WSL and VScode setup guide#Github Login|Github Login]]

# Install WSL via powershell
- Following instructions from [Microsoft Learn](https://learn.microsoft.com/en-us/windows/wsl/install)
- Open the Start menu (or press the windows key)
- Type `powershell` into the search bar
- Click `Run as Administrator` ![[powershellRunAsAdmin.png|500]]
- Run the following command in the powershell window
	- `WSL --install`


# Install and Setup WSL Ubuntu
- [Use this Link](https://www.microsoft.com/store/productId/9NZ3KLHXDJP5?ocid=pdpshare) to open the Microsoft Store and download `Ubuntu 24.04.1 LTS` 
- Open Ubuntu and a Ubuntu terminal application should open![[Pasted image 20241122114611.png]]
- Follow the onscreen prompts to create a username and password (this login information is separate from windows and ONLY for the Ubuntu terminal)
	- **Note: When entering a password the text cursor WILL NOT MOVE, this is expected and the input field is active and your keystrokes are being properly recorded**
- After the window saying `Installation complete`
	- Run following commands
		- `sudo apt update` (you will be prompted for the password you just made above)
		- `sudo apt full-upgrade -y`
	- Ubuntu is now installed and up to date![[ubuntuInstallComplete.png]]
# Install Miniconda in Ubuntu
- Following the instructions for [installing miniconda on Linux](https://docs.anaconda.com/miniconda/install/#quick-command-line-install) 
- In the `Ubuntu 24.04.1 LTS` command line run the following:
	- `mkdir -p ~/miniconda3`
	- `wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh`
	- `bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3`
	- `rm ~/miniconda3/miniconda.sh`
- After installing, close and reopen your terminal application or refresh it by running the following command:
	- `source ~/miniconda3/bin/activate`
- Initialize conda on all available shells, run the following command:
	- `conda init --all`
- Close and reopen the terminal window and run the following
	- `conda --version`
	- If it prints out `conda XX.X.X` (where X is a version number) then it is properly installed
## Setup Conda environment
- The following steps will be environment specific for you project but I will add a few notes 
- Using the Ubuntu Terminal:
	- If you have an existing project/repo with an `environment.yaml` (a file that has names all library dependencies for a project)
		- [Follow Creating an environment from environment.yml file](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file)
	- Otherwise, follow [Create an environment with commands](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-with-commands)

# VScode Setup
- Open the following link to download [VSCode](https://code.visualstudio.com/download)![[VSCodeDownloadScreenshot.png|500]]
- Follow installer instructions and open VScode
- Navigate to Extensions
	- Type `WSL` into the search bar
	- Click the `Install` button (shown where`Uninstall` is in the screenshot)![[vsCodeExtensionsScreenshot.png]]
	- Repeat the same steps for the `Jupyter Notebooks` and `Python` extensions


# Connect to WSL using VSCode
- Click the `Open a Remote Window` button in VScode (looks like two arrows in bottom left corner)
- Click `Connect to WSL using Distro...` -> `Ubuntu-24.04` ![[VScodeConnectToWSL.png]]
- Your VScode is now running in the Ubuntu environment and using its file directories
	- This means any project files or changes you make in VScode happen in this Ubuntu directory![[VScodeconnectedtoWSL.png]]
- The VSCode terminal window should also be running in the Ubuntu environment meaning you can run terminal commands inside VScode instead of using the Ubuntu window
	- Note: VScode will activate your WSL instance when it connects to the remote. 
		- You do not need to leave the Ubuntu terminal application open when running notebooks in its environment

# Adding or Removing files from Ubuntu environment
- Open `File Explorer` and navigate to the `Linux` ![[LinuxFileExplorer.png|500]]
- If the Linux does not show in the side navigation bar you can 
	- Click the path bar at the top 
	- Type `\\WSL$` and all WSL installed Linux distros will appear![[Pasted image 20241127143824.png]]
- Your VSCode opens into your `/home/<User>/` directory, you can navigate to the same directory following `/Ubuntu-24.04/home/<User>/`
	- Right clicking this folder and using `Pin to Quick Access` is recommended to keep it in the left-side navigation bar
- You can copy and paste files into this folder via `File Explorer` similar to any other windows folder
- Now you can click `Open Folder` or `Clone a Repo`
	- `Open Folder` will use VScode's search bar to show files in the `/Ubuntu-24.04/home/<User>/` directory![[WSLVScodeOpenOrClone.png]]
## Open or Create a Jupyter Notebook file using Conda 
- If at any point VScode asks to install something such as `ipykernel` you can just click install and restart VScode if necessary	
- Step 1: Open the notebook (or right-click and create a file ending in `.ipnyb`)
- Step 2: Click Select Kernel (a kernel is already selected in the picture)
- Step 3: Click Python Environments![[selectKernel.png]]
- Step 4: Select the name of the Conda Environment from the list (either the name you created above or it can be found in you `environments.yml` file under `name: ` (in the example below the name is `tot`![[selectEnv.png]]
## GitHub Login
- You should be able to login and setup GitHub by logging in via VScode by clicking the `Accounts` button on the left-side bar near the bottom (little person icon)
	- if you get an error about setting a git username and email you can set it with these commands in the VScode terminal
	- Be sure to replace your actual username and email in the quotations
		- `git config --global user.name "Your Name"`
		- `git config --global user.email "you@example.com"`