# Installation Guide
### Basics
1. Install ModEngine 2 or ModEngine 3 and locate the 'mod' folder.
2. Move the contents of the zip into the mod folder.

    A. If requested to overwrite files, deny. Merging will be handled in the next step.

### Scripts-Data-Exposer-FS.dll by ElaDiDu
*If installed already, skip this step*

3. Register the 'Scripts-Data-Exposer-FS.dll' in your ModEngine 2 or 3 installation.

    A. For ModEngine 2, add `"mod/Scripts-Data-Exposer-FS.dll"` to your `external_dlls` table.
    
    B. For ModEngine 3, add `path = 'mod/Scripts-Data-Exposer-FS.dll'` as a new `[[natives]]` registration.

### c0000.hks
*If you did not have a `action/script/c0000.hks` prior to installing this, skip this step*

4. Add the following code snippet right above the line that says `global = {}` near the bottom of the file:

    ```lua
    script_dir = debug.getinfo(1, "S").source:sub(2):match("(.*/)"):gsub("/", "\\") .. "modules\\"
    pcall(loadfile(script_dir .. "LoadingScreens.hks"))
    ```

The End


# How to use
Open up `mod/action/script/modules/LoadingScreen.hks`

The file seperated into 3 parts. For basic use you only ever have to worry about the first part: The Main Table

In here you can do various things

- Removing or commenting out existing loading screens so they have no more chance of showing up, in Lua you comment out a line by adding -- in front of it.

- Modify the chances of how common a loading screen is, the higher the weight the more chance it has to show up sooner. 

  Setting it to 0 will work the same as removing the line.
  
- Tie an eventflag to the loading screen, this will make it so the loading screen will not appear untill the eventflag is set to true. 

  When a flag is set to true it will forcably be set to be the next loading screen in the queue.
  
- Register new loading screens, loading screen 35 is set up as an example. You will also need to add the actual image in `mod/menu/hi/00_solo`

  Loading screen numbers do not need to be sequential, but do need to follow the existing pattern from Vanilla
  
  So in 00_solo you need to add for example: MENU_Load_00035.tpf.dcx in order to use loading screen 35. You could also start your loading screens at 100 or something if you want.
  
  For implimenting a new loading screen *.tpf, follow existing tutorials and protocols to register a new image.

Modify things to your heart's contend but know that you will need at least 1 loading screen to be accessible at all times.

If you have 0 loading screens that are possible to use, the system will refuse to function and will follow Vanilla's protocol for handling loading screens, which will not use loading screens above 34


# Credits
Special thanks to:
- chainfailure / vswarte for finding the correct locations in memory
- ElaDiDu for creating the Scripts-Data-Exposer-FS.dll
