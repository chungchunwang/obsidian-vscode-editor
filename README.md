# obsidian-vscode-editor
This adds VSCode as a window inside of Obsidian, allowing you to switch to a VSCode editor when editing a file inside of Obsidian. This is based off of u/stat30fbliss's showcase post [here](https://www.reddit.com/r/ObsidianMD/comments/yfxdlb/vs_codeserver_in_obsidian/) on Reddit. The following is basically a set of instructions and files I put together while trying to recreate what he/she made.

*Note: These steps require you to install Docker and have community plugins enabled in Obsidian.*

# Instructions

## 1. Install Docker.
If you haven't already, go [here](https://www.docker.com/) and install Docker. It is a tool that allows you to run containers - basically small virtual machines. We will host VSCode from such as container.

Here is an [article](https://medium.com/devops-with-valentine/how-to-install-docker-on-windows-10-11-step-by-step-83074a80e6f9) that has more detailed instructions on how to install Docker. 

## 2. Add the Custom Frames and the 

# Install whatever extension you will need below. You can download the extension file from the VSCode marketplace website.
# You can download most extensions through the UI, but some common extensions are missing from the marketplace code-server uses.
# You can do this with the command: code-server --install-extension <path to extension file>
# For example, if you need to debug C++ code, you can install the C/C++ extension (delete the following line if you do not need this).
COPY ms-vscode.cpptools.vsix ms-vscode.cpptools.vsix
RUN code-server --install-extension ms-vscode.cpptools.vsix
