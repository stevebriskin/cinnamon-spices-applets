# The Network Usage Monitor Applet (NUMA)

## Summary

The Network Usage Monitor Applet (NUMA) enables one to continuously display the speed and data usage on a selected interface. It is intended to make monitoring of mobile connections by USB Mobile Internet Dongles, through phones by bluetooth and by Mobile Wifi (MiFi) units easy to accomplish. To this end, a maximum data and easily changed Alert level can be set for the current connection. There are also a number of cumulative data monitors to track total usage with offsets and corrections as required. It builds on the Network Speed Monitor Applet project by adreadec.

## Special Requirements:

   * For the basic facilities the ```gir1.2-gtop-2.0``` library __must be installed__ or the applet will not load and a notification will be displayed. It can be installed by the synaptic package manager or with the terminal command:
                      ```sudo apt-get install gir1.2-gtop-2.0```

   * For full facilities including use of notifications, audible alerts and statistics the ```gir1.2-gtop-2.0 vnstat vnstati zenity sox libsox-fmt-mp3``` libraries must be installed. They can be installed  by the synaptic package manager or with the terminal command:
            ```sudo apt-get install gir1.2-gtop-2.0 vnstat vnstati zenity sox libsox-fmt-mp3``
   * Cinnamon Version 2.2 or higher ie. It can be used with all supported versions of Mint.
   * Version 3.2.4 require the NMClient and NetworkManager libraries to be in use as was the case in Mint versions up to 18.3 and most other current distro versions at that time.
   * Version 3.2.5 will switch to the more recent NM library if the NetworkManager Library is not available.
   * Version 3.2.6 and higher can only use the new NM libraries when Cinnamon 4.0 or higher is in use to avoid potential segfaults in Cinnamon 4.0. This should support all current Linux Distributions which support Cinnamon 4.0.

## Features:

  * **The Applet:**
       + Continuously displays Upload and Download rate in a fixed width 'steady' display
       + The Applet Background color is:
          - Black when Current Interface not active
          - Green when Current connection and interface has provided data
          - Orange when the Alert level (as percentage of the Data Limit) has been exceeded
          - Red when the Data Limit for the current connection has been exceeded
   * **Hover over Applet:**
       + Displays continuously updated Upload and Downloaded data usage for the current connection
   * **The Context Menu (Right Click):**
       + Displays all the interfaces managed by the Network Manager Applet
       + Identifies any Active interfaces within Network Manager
       + Allows the selection of the interface to be monitored from those manged by Network Manager.
       + Allows the selection of an interfaces not managed by properly by Network Manager and/or interfaces  for a connection initiated outside Network manager (ppp0 and bnep0). (bnep0 needs v20_2.6.0 or higher)
       + Identifies the interface which has been selected for monitoring.
       + Allows updating of the list of Network Manager Interfaces (e.g. after a dongle has been inserted or a bluetooth connection made)
       + Enables the Cumulative Usage Monitors to be reset and the date and time of reset displayed.
       + Provides links to:
          - The NUMA Settings screen.
          - The Gnome System Monitor
   * **Left Click Menu:**
       + Displays continuously updated Uploaded and Downloaded Data for the Monitored Interface.
       + If Alerts are enabled:
          - A slider to adjust the Alert level as a percentage of the Data Limit
          - A display of the exact Alert level percentage and the Data Limit
       + For each Interface where cumulative monitoring is enabled:
           + The interface and Cumulative Usage
           + A comment (entered in Settings) to remind one of when it was set/reset and the value when set/reset.
   * **The Settings Screen allows:**
      + Setting the Update Frequency (1 to 5 seconds)
      + The Resolution of displayed upload and downloads (0 to 2 decimal places)
      + Change the units for Data Limits and Cumulative Offsets between Mbytes or Gbytes 
      + Setting an interface to use as Default if no other interface is active at start-up - for Wifi hotspots and Mobile Broadband where the connection is manual.
      + Enabling Alerts on the current monitored interface and setting the Data Limit for the current connection on that interface and
           - setting the Alert Level as a percentage of the Data Limit by a slider (duplicated in the left click menu as it is frequently used.
           - Enabling each of three Cumulative Usage Monitors
    Setting an offset for each Cumulative Usage Monitors (v20_2.6.0 or higher)
       + Switching on a Long Term Statistics Display (Requires vnstat and vnstati to be installed)
       + Enabling Actions when the Current Data Usage Limit is exceeded:
          - __Do nothing other than put up a standard Cinnamon Notification__ - this displays for 5 seconds or so and ends up in the notification tray - very easy to miss.
          - __Display a high priority Notification__ - this displays on to of other windows until you clear it but does not go into the notification tray - still easy to miss from a distance.
          - __Display a full screen Modal Dialog__ - this is techie term (look it up on Wikipedia) and the result is the whole screen is blacked out with an information box and button to clear it in the middle and uses the internal capabilities of Cinnamon. It is impossible to miss if you are at or close to the machine.
          - __Run a shell script which lives in the applet folder and is called alertScript__ - this can be customised by the user and the example plays a system sound file for 6 seconds (using Sox) , puts up a warning box using Zenity and sends a standard notification so you have a record in the notification tray.
          - __Suspend the Machine after a brief period during which you can abort__. This is also implemented by a script (suspendScript) so the user can fine tune it but the version provided uses Zenity for the warning message which has a 30 second timeout to allow you to abort. Another message is put up before suspending which should be on display when you wake up the machine.
         - __Disable Networking for all connections managed by the Network Manager__.  This puts up a warning message and you can abort for a short period by clicking the Applet - not the OK button on the warning screen.
   * Set a delay before disabling Network Connections
    Enable a warning sound
       + Set the sound file to be played
   * Add or hide the Advanced functions from Housekeeping drop down menu

## Additional Configuration

### Styling

The display width, justification and font details are set using an external Cascading Style Sheet (.css) file which is in the main folder (usually ```~/.local/share/cinnamon/netusagemonitor@pdcurtis/stylesheet.css```).

The settings in this css file govern the width of the Applet and the font. Changes may be required with some themes to avoid the display width being exceeded which leads to jitter with high network speeds and resolutions or to allow a reduced size width to save panel space. The latest version also allow the backgrounds to be configured using this css file to optimize to a particular theme although the defaults work well on most popular themes.

Note: These settings will be overwritten if the applet is reloaded.

### Interfaces monitored by the optional ```vnstat``` display.

The system program vnstat which provides the option of a graphic history of data used is automatically set up when it is installed to monitor the network devices/interfaces installed in the machine at the time. It is possible to add additional USB network devices and possibly bluetooth devices to the list of monitored interface ```man vnstat``` in a terminal will give details.

## Status

The author is committed to maintaining and developing the applet. The applet is based on a well tried core from the netspeed applet and has been tested on various systems initially running under Mint 15 with a variety of themes. The current Version has been tested with Cinnamon 2.2 - 3.6 under Mint 17 - 18.3. But see Warnings above about use under Fedora 27 which have yet to be addressed.

## Translations and other Contributions

The internal changes required in the applet to allow translations are being implemented but no translations are available at this time. Translations are usually contributed by people fluent in the language and will be very much appreciated. Users please note I am unable to take responsibility for the accuracy of translations!

Although comments and suggestions are always welcome any contributions which are contemplated should follow discussion. Changes can have many unintended consequences and the integrity of the applet is paramount. Unsolicited Pull Requests will never be authorised other than for urgent and critical bug fixes or from the Cinnamon Team. 

Thanks are given for the very useful contributions from @collinss and @Odyseus to help harmonise the menus with other applets.

## Manual Installation:

   * Download from Cinnamon Spices
   * Unzip and extract folder netusagemonitor@pdcurtis to ~/.local/share/cinnamon/applets/
   * Install the additional programs required.
   * Enable the applet in Cinnamon Settings -> Applets
   * You can also access the Settings Screen from Cinnamon Settings -> Applets


### Version information prior to the changes introduced by the new Cinnamon Spices Web site in January 2017

There is a change log in the applet folder called CHANGELOG.md which can also be accessed through the Context (Right Click) menu in the Housekeeping sub-menu. The initial  development was carried out on Github along with my other applets at [github.com/pdcurtis/cinnamon-applets](https://github.com/pdcurtis/cinnamon-applets)

### Contact

The author can be contacted via the comments on the [Cinnamon Spices Web Site](http://cinnamon-spices.linuxmint.com/applets/view/141), however that does not automatically notify me so if you want a rapid response please also alert me via the [Form at www.pcurtis.com](http://www.pcurtis.com/contact_form.htm?applets). On github, mentioning @pdcurtis in any conversation will cause it to be emailed to me.

