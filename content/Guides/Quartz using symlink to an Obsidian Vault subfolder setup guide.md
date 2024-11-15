## Why you would want to set this up
[Quartz](https://quartz.jzhao.xyz/) by default can be tricky to set up with an existing Obsidian Vault where you would only like to share a single folder to be published. 

Using a symlink, you can keep your quartz git repo (with its thousands of NodeJS files) completely separate from you Obsidian Vault and prevent time wasted syncing and storing all of those files. This also prevents some issues with files getting lost with git and obsidian sync fighting each other.

Quartz has support for this but afaik there is no explicit guide in the docs for setting it up so I wrote one here.

For example, my Obsidian Vault has tons of other notes in other categories. I would like to only export content from the `Vault/Personal/Digital Garden/content` folder to my hosted quartz page without having to place the entirety of the nodeJS files in `Vault/Personal/Digital Garden` causing Obsidian to sync and keep track of them. 
![[content folder location.png]]


I can clone my quartz repo somewhere else like `~/Documents/quartz` and set `/quartz/content` to link to the `Vault/Personal/Digital Garden/content` folder and allow them to sync independently.

## Setup Guide:
- If you haven't already, install [NodeJS](https://nodejs.org/en)
	- if using windows installation is self-explanatory
	- for Arch Linux you can follow [[Install NodeJS on Arch Linux with nvm]]
- Fork [quartz](https://github.com/jackyzha0/quartz) to a location OUTSIDE of your Obsidian Vault
	- Following the [Getting Started](https://quartz.jzhao.xyz/#-get-started) section
		- `git clone <your forked repo URL>`
		- `cd <your forked repo name>`
		- `npm i`
		- Here is where we deviate:
			- Cut the `/content/` folder out of the quartz repo and place it to a location inside of your obsidian vault 
				- e.g. `Vault/Personal/Digital Garden/content`
		- When running `npx quartz create`:
			- When it asks `Choose how to initialize the content in <your forked repo name> make sure to select 
		- ![[Pasted image 20241114151239.png]]
		- When it asks `Enter the full path to existing content folder`:
			- Find the path to the `/content/` folder in the Obsidian vault
				- Dragging the folder into my terminal DID NOT WORK, it added quotes and errored
				- You can right click the folder in a file explorer and select `Copy as path` in windows or `Copy Location` in Dolphin and it should work
					- Mine looked like the following with NO QUOTES
					- `/home/awkwabear/Documents/Vault/Personal/Digital Garden/content`
		- ![[Pasted image 20241114151552.png]]
		- When it asks `Choose how Quartz should resolve links in your content. This should match Obsidian's link format.
			- Obsidian defaults to shortest path which is what I used 
				- You can check in Obsidian settings here under `New Link Format`
				- ![[Pasted image 20241114152242.png]]
		- ![[Pasted image 20241114152055.png]]
- After doing this, everything should be good to go. You can follow the rest of quartz instructions to host your page
	- You can use the quartz git repo folder to sync to your webpage and host
	- You can separately write content into your vault without storing all the nonsense NodeJS pages
