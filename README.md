# desktop

ambxst <br />
vicinae -> matugen theme -> remove hover (colors.list.item.hover) and set foreground for selection as secondary_container <br />
spicetify -> visualizer <br />
wallpapers <br />
fastfetch <br />
solarust, metropolis <br />
spotibye/SpotiFLAC <br />
qylock <br />
hyprselect <br />
asciiquarium <br />
plymouth <br />
cursor <br />
[netorbit](https://github.com/ZXCurban/NetOrbit) <br />
pipes, cava <br />
lazygit <br />
macos theme icons <br />
superfile <br />
apple-emoji-ttf <br />
waydroid  <br />
kitty -> optionally change ambxst kittygenerator and set cursor color as primary <br />
set env QT_QPA_PLATFORMTHEME to kde <br />
optionally (would recommend) fix css in gtk 4 for theme colors <br />
apple fonts <br />
kopuz <br />
vesktop (and use ambxst theme)
use [matugen themes](https://github.com/InioX/matugen-themes) to customize everything; EVERYTHING. firefox sites, spotify, vscode ...

## fucking gpu drivers; make sure to install them; i thought they already had it in base

## Cool things ig
[engine simulator (run it through wine)](https://github.com/Engine-Simulator/engine-sim-community-edition#installation-Instructions)

## install these
hardware accelearation - intel-media-driver

## downlaod profile-sync-daemon to prevent read write issues and also increase speed - uses more ram

## for davicni resolve
install opencl-mesa
https://www.reddit.com/r/Fedora/comments/1l05jcf/davinci_resolve_on_intel_igpu_fix_unsupported_gpu/
archive:
```
Background

I did a fresh install of a Fedora 42 to get Davinci Resolve working. I'm on a ThinkPad T480 with an Intel UHD Graphics 620 and I just couldn't get it working. The most common solution I found was to install the intel-compute-runtime package, but it no longer supports Intel's 9th gen graphics. Whatever I did, clinfo would just return: Number of platforms 0

They do offer a legacy version on their github that you can compile yourself, but I ended up in dependency hell - hence the fresh reinstall. Anyway - I found a way to make it work.
Pre-requisites - installing DR

I won't cover how to install Resolve itself. Since we're all on Fedora here, I recommend you use Davinci Helper if you're not sure how to go about it. You can find it here.

The rest of this guide is how to solve the problem I had - the "Unsupported GPU Processing Mode" pop up after it's been successfully installed due to OpenCL not working properly.
1. Install rusticl

Open up your terminal and run

sudo dnf install mesa-libOpenCL mesa-dri-drivers clinfo
2. Test it

Set an environment variable for the current session

export RUSTICL_ENABLE=iris

After this, run clinfo | grep "Device Name" and you should get a line showing the following (well, the name of your iGPU):

Device Name Mesa Intel(R) UHD Graphics 620 (KBL GT2)
3. Make it permanent

If it works, you can import this to your bash shell and thus make it permanent by running the following command:

echo 'export RUSTICL_ENABLE=iris' >> ~/.bashrc

Then reload the shell

source ~/.bashrc

Run clinfo | grep "Device Name" again to make sure it worked. If everything went well, you should now see the name of your iGPU

Device Name Mesa Intel(R) UHD Graphics 620 (KBL GT2)
4. Start Resolve in terminal

If you've installed it and tried opening it, you're probably still experiencing the "Unsupported GPU Processing Mode" pop-up. Try running the program through the terminal by entering

/opt/resolve/bin/resolve

It should then start up normally and recognise your GPU. If this doesn't work, I'm not sure how to help you. If it does work, the problem lies in the .desktop file.
5. Replacing the .desktop file

Inside /usr/share/applications/ you should find a file called com.blackmagidesign.resolve.desktop - this is the cause of the problem.

We don't actually need it, and can instead make our own. To remove the faulty .desktop file, run

sudo rm -f /usr/share/applications/com.blackmagicdesign.resolve.desktop

Replace it with a new one within your home folder by running

nano ~/.local/share/applications/resolve.desktop

Once inside nano, paste the following:

    [Desktop Entry]
    Name=DaVinci Resolve
    Exec=env RUSTICL_ENABLE=iris /opt/resolve/bin/resolve
    Icon=/opt/resolve/graphics/DV_Resolve.png
    Type=Application
    Categories=AudioVideo;Video;Editing;
    StartupNotify=true
    Terminal=false

Press ctrl + W and then Y to confirm. This will save the file.

Now, update your desktop database for the directory in which you placed the .desktop file by running

update-desktop-database ~/.local/share/applications

If the old .desktop file is still showing up, try logging out and in again. It should disappear.

An important note is that placing the custom .desktop configuration within the existing /usr/share/applications/com.blackmagicdesign.resolve.desktop file does not work. It has to be in your home folder. I'm sure you can probably configure the permissions or something as well, but this method works just fine on my laptop and I'm not about to go digging around and ruin it again. 
```
