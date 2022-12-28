# obsidian-vscode-editor
This adds VSCode as a window inside of Obsidian, allowing you to switch to a VSCode editor when editing a file inside of Obsidian. This is based off of u/stat30fbliss's showcase post [here](https://www.reddit.com/r/ObsidianMD/comments/yfxdlb/vs_codeserver_in_obsidian/) on Reddit. The following is basically a set of instructions and files I put together while trying to recreate what he made.

*Note: These steps require you to install Docker and have community plugins enabled in Obsidian.*

# Instructions

## 1. Install Docker.
If you haven't already, go [here](https://www.docker.com/) and install Docker. It is a tool that allows you to run containers - basically small virtual machines. We will host VSCode from such as container.

Here is an [article](https://medium.com/devops-with-valentine/how-to-install-docker-on-windows-10-11-step-by-step-83074a80e6f9) that has more detailed instructions on how to install Docker. 

## 2. Setup Docker-Compose
Download this repository by going to Download->Download as Zip File at the top of this page. Then unzip the file and find the System folder inside. Drag that into your vault, wherever you want. I think System is a good name for it, but you can rename it to whatever you like.

Now, there are some settings that you can change. First go to the .env file, opening it with some editor. Here you can set whatever port your VSCode will run on (the default 8080 should be fine as long as it doesn't conflict with anything else on your system). You can also set the password for sudo in the VSCode terminal. Most importantly, you **must** provide the root directory of your vault. Make sure this is correct as it will vary depending where you put the System folder. Additionally, you can set the Timezone of the Linux server ([using the TZ codes](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)).

Next, open up a terminal in your System folder and run `docker-compose up`. After a long time and a lot of downloading, an instance of VSCode should be begin hosting at localhost:8080 (or whatever port you changed it to). If this worked, press `Ctrl-C` in the console to stop the hosting.

## 3. Add the Custom Frames and Shell Plugins to Obsidian.
Go to Setting (Gear Icon) -> Community Plugins (Make sure you have restricted mode off so you can install community plugins) -> Browse.
Here, search for the plugins Custom Frames and Shell commands. Install and enable them.

## 4. Configure Custom Frames Settings
Go to Setting (Gear Icon) -> Custom Frames. Click on the Add Frame button, then click Show Settings on the newly created frame. Give it a name (I suggest "VS Code"), an icon, and a url of "localhost:8080" (change the port at the end of this if you modified it earlier). Set the Add Ribbon Icon option to be true so that you can open VSCode from the ribbon. Also click Disable on Mobile (this only works on a system with docker) and Open In Center (so that VSCode won't be crammed to one side). Restart Obsidian so that the changes will register.

## 5. Configure Shell Commands Settings
Go to Setting (Gear Icon) -> Shell Commands. Click on the New Shell Command button, then type the command `docker-compose up` into it. Click the events button for that command (third from last button), which will open up a page with an array of trigger events. Select Obsidian Starts, then close this page.

Click on New Shell Command to create another command. This time type `docker-compose down` into it. Click the events button for that command, and this time select Obsidian Quits.

Finally, we need to set the directory from which these commands run. Go to the Environments tab and under Working Directory put the path for your System folder (or whatever you renamed it to).

## 6. Finished!
Now, close and reopen Obsidian. There should be a new Ribbon button on the side to open VSCode (it should have the icon you set in an earlier step). Click that, and VSCode should boot up in a window. If you click this too quickly, ~5-10 seconds after Obsidian boots up you may be met with a white screen as the Docker container is still starting up. Afther that period the button should work! To not clog up your computer's resources, the container should close when you close Obsidian.

## Installing Extensions
You will notice that in the extension store there are missing a lot of common extensions. This is because the default VSCode extension library is proprietary. You can, however, manually download extensions from the [VSCode marketplace](https://marketplace.visualstudio.com/vscode) as files and install them manually. Follow the following steps to do so.
### 1. Search for the extention you want.
As the title states, find the extension and open its page.
### 2. Download the extention as a file.
On the sidebar of the page you should see a Resources section. Under there should be a link entitled Download Extention. Click that and you should begin downloading a .vsix file. Do not click the green Install button, that does not work.
### 3. Install the extension.
Drag the extention file into your vault. Inside of your VSCode panel, open up a new terminal. Type `code-server --install-extension <location of your extention file>` and hit Enter. The extension should install to VSCode.


# Final Thoughts
A bit of a shameless plug here, but if you found this helpful please star! While the final product for this was very simple this took me a lot of time (mainly because I went on bit of a side tangent adding other stuff to the DockerFile that I later found was useless). Also many thanks to u/stat30fbliss, as this was his idea!
