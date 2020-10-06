# Fusion 360 CAM Batch Post Process Add-In
#### NEW! Fixes tool change restriction in Fusion 360 for Personal Use
See section below.

### Introduction
This add-in for Fusion 360 will post-process all CAM setups at once.
Each setup is put in a file with the name of the setup. You can
optionally use a special setup naming convention to put files in
subfolders. You can also put sequence numbers on the name to maintain
the order of operations.

The add-in creates a new command in the Manufacture workspace next to
the native Post Process command called Post Process All:

![Post Process All](https://raw.githubusercontent.com/TimPaterson/Fusion360-Batch-Post/master/resources/Command/32x32.png)

Clicking this command will bring up the following dialog:

![Dialog Image](https://raw.githubusercontent.com/TimPaterson/Fusion360-Batch-Post/master/ReadMeImages/DialogImage.PNG)

The first time you run this command, the Output Folder and Post Processor
fields will be blank. You must set both of these fields before you can
click OK. Once the command has been run, all settings will be saved in
the design. New designs will also be given default settings.
### Subfolders
You can put the output files in subfolders by using a colon (":") in
the name. The part of the name to the left of the colon is the folder
name; multiple colons result in nested subfolders.

Here is an example of a design with three components. The name of the
component appears first, then a colon and the name of the setup for
that component:

![Setup Image](https://raw.githubusercontent.com/TimPaterson/Fusion360-Batch-Post/master/ReadMeImages/SetupImage.PNG)

When you run the Post Process All command, it will create three
subfolders in the output folder, named "Cover", "Block", and "Insulator".
Within these subfolders will be five, three, and five G-code files
respectively with names like "first long edge", "second long edge", etc.
### Sequence Numbers
A sequence number can be added to the front of each file name. This
provides a reminder of the order of operations and will generally
keep the files sorted in that order. Sequence numbers start at 1 for
each folder.

In the above example, when adding sequence numbers the files in
the "Block" folder would have the names "1 first edge" and "2 second
edge".
### Fusion 360 for Personal Use
The free version of Fusion 360 now has some limitations on G-code
output: It will not support tool changes, and it slows down all
moves to feed rate. This add-in can work around the tool change
limitation and makes a first step in restoring rapid moves.

In the Personal Use section of the add-in dialog, you will find
the option to break each setup into individual operations. This 
is required if you have the free version of Fusion 360 and there
is a tool change in any setup. The add-in will combine the G-code
for each operation of a setup back into a single file for that
setup, hiding this limitation.

In addition, you can also select the option to change the first
Z moves in each operation to rapid (G0) moves. Currently this
affects only the first one or two moves, and should be reviewed
before use. Hopefully this can be extended to more eligible moves.
### Installation
To install, start by putting the PostProcessAll.* files along with
the "resources" subfolder into a folder on your machine. This can
be a Git repository or just a copy of the files. (The ReadMe.md
file and ReadMeImages folder are not required.)

In Fusion 360, go to the Tools tab in the Design workspace, or the
Utilities tab in the Manufacture workspace. Select the
Add-Ins command, which will bring up the Scripts and Add-Ins dialog.
Switch to the Add-Ins tab, then click the green "+" to add a new
add-in. You can now browse to the folder in which you placed the
Post Process All add-in files.

Once the folder is selected, you will be returned to the Add-Ins dialog
and find that PostProcessAll now appears in the list of "My Add-Ins".
Select it in the list, ensure "Run on Startup" is checked, and then
click the Run button. That's it! Fusion 360 will load the add-in every
time it starts up.

To see the new command, go to the Manufacture workspace and select the
Milling or Turning tab. The command appears on the toolbar next to
the native Post Process command. It also appears in the Actions
drop-down menu.
### Issues
If the command fails, run it again. There seem to be occasional timing 
issues that usually resolve themselves.

The concatenation and modification of G-code has been only been lightly
tested and with just one post processor (Tormach). Given that there are
very specific assumptions about what the G-code input will look like,
it would not be surprising to find problems come up. Feel free to report
them on the Issues page, and include the G-code files.
