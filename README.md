# DynamicLOD_ResetEdition v0.5.3

Based on muumimorko's idea and code in MSFS_AdaptiveLOD, as further developed by Fragtality in DynamicLOD and myself in MSFS2020_AutoFPS and MSFS_AutoFPS.<br/>

Now fully compatible with MSFS 2020 and 2024 in the one app, this app builds upon the functionality provided in DynamicLOD, which aims to improve MSFS performance and smoothness by dynamically changing the TLOD and OLOD based on the current AGL, and provides additional features such as:<br/>
- Automatically detects and displays the MSFS version in use and keeps separate settings for each MSFS version and a single log file for both.
- Remembers which MSFS version you last used the app with and will start up next time with the settings for that MSFS version.
- Simultaneous PC, FG (native nVidia, MFG, FG mod, FSR3 or Lossless Scaling), and VR mode compatibility, including correct FG FPS display, and separate FPS targets for each mode,<br/>
- Optional LOD updates in cruise,<br/> 
- Optional predictive incremental steps between LOD changes to improve smoothness,<br/>
- Optional cloud quality decrease with FPS Adaption,<br/>
- Enhanced FPS Adaption control,<br/>
- Automatic pause when MSFS loses focus option, particularly useful if using native nVidia FG due to varying FPS when MSFS gains or loses focus,<br/>
- Automatic FPS settling timer on MSFS graphics mode and focus changes to allow FPS to stabilise before being acted upon,<br/>
- Auto future MSFS version compatibility, provided MSFS memory changes are like in previous updates,<br/>
- Custom profile naming,<br/> 
- Auto installation of app updates (optional except for mandatory updates),
- Auto disabling of Dynamic Settings in MSFS 2024 while this app is active, to prevent settings contention,
- Auto restoration of original settings changed by the utility,<br/>
- Enhanced saving and restoration of MSFS settings by the app to better withstand MSFS CTDs,<br/>
- Streamlined log entries,<br/> 
- Removal of redundant features, and<br/>
- Minor UI changes.<br/><br/>

**Really, really important:**
- Do not even mention, let alone try to discuss, this app on the MSFS official forums, even in personal messages, as they have taken the view that this app modifies licenced data, regardless of how harmless the way in which the app does it, and is therefore a violation of their Terms of Service and Code of Conduct for that website. If you do so, your post/personal message will be flagged by moderators and you may get banned from the MSFS official forums. You have been warned!

Important:<br/> 
- This utility directly accesses active MSFS memory locations while MSFS is running to read and set OLOD, TLOD and cloud quality settings on the fly. From 0.3.7 version onwards, the utility will first verify that the MSFS memory locations being used are still valid and if not, likely because of an MSFS version change, will attempt to find where they have been relocated. If it does find the new memory locations and they pass validation tests, the utility will update itself automatically and will function as normal. If it can't find or validate MSFS memory locations at any time when starting up, the utility will self-restrict to read only mode to prevent the utility making changes to unknown MSFS memory locations.<br/>
- As such, I believe the app to be robust in its interaction with validated MSFS memory locations and to be responsible in disabling itself if it can't guarantee that. Nonetheless, this utility is offered as is and no responsibility will be taken for unintended negative side effects. Use at your own risk!<br/><br/>

Which app should I use? DynamicLOD_ResetEdition or MSFS_AutoFPS?:
- Essentially both apps are intended to give you better overall performance but with different priorities to achieve it that result in a slightly different experience.  They both allow a lower TLOD down low and on the ground, when your viewing distance reduced anyway so the visual impact is minimal, and a higher TLOD when at higher altitude and not in close proximity to complex scenery or traffic. They also adjust OLOD and Cloud Quality but TLOD is usually the most important determiner of performance at these two extremes.
- Where they differ is that DynamicLOD provides user set tables for LOD changes at specific altitudes, giving the user precise control over when and where these changes take place such that they can optimise them to their particular flight activity they normally do, and can set a specific profile for each one. The price of such precise control is that the user must be intimately familiar with LODs to be able to tune a variety of settings in the app for the best outcome and this can be a bit daunting for more casual and non-technical users.
- Alternatively, AutoFPS seeks to automate these changes as much as possible based on a target FPS and a minimum and maximum LOD range within which to automatically adjust. This results in a much simpler and generally similarly acceptable user experience compared to DynamicLOD. Nonetheless, AutoFPS tends to make constant small changes to TLOD, much more than DynamicLOD does, and this can induce stuttering on older hardware as it struggles to manage even small scenery changes. In these cases, the user would be better off using DynamicLOD in a more manually tuned approach. 

How does this app work for Frame Generation (FG) users?
- The app does detect correct FG FPS when FG (native nVidia or FG mod) is enabled in MSFS, however FG is only active when MSFS is the focused window and becomes inactive when not, through your graphics driver not this app.
- To see correct MSFS FG FPS, use the app's "On Top" option to overlay this app over MSFS and give MSFS the focus.
- If MSFS FG is being incorrectly reported as enabled by the app, the likely reason is that either the FG mod had been installed and removed or you have disabled Hardware Accelerated Graphics Scheduling under Windows settings and the now the now greyed out MSFS FG setting may show that it is off but it is still set to on internally to MSFS. To fix, change the DLSSG line in your UserCfg.opt file to be DLSSG 0.
- Lossless Scaling (LS) FG, including the scaling multiplier used, is also detected and the correct LSFG multiplied FPS is displayed.
  - Make sure your LSFG app is updated to the latest version that supports LSFG 3.0 (2.13.2 or later).
  - The app will first try to use an LS profile with the specific name MSFS2020 or MSFS2024, depending on which MSFS version is currently in use, to obtain these settings.
  - If such an MSFS2020 or MSFS2024 profile does not exist then the settings in the first profile found in the config file, usually named Default, will be used.
  - When adaptive frame generation is detected, a base FPS will be used for the target FPS because the frame generation multiplier is variable and is not currently detectable.
  - If you make changes to your LS settings after starting a flight, press AutoFPS's Reset button so that AutoFPS can redetect them correctly.
- FSR3 FG is now supported for MSFS 2024 as of SU2.
  - Although FSR3 FG can be implemented with an adaptive multiplier, MSFS currently implements it with a fixed 2X multiplier that is active regardless of whether MSFS has the focus or not.
- Multi Frame Generation, available only for users with 5000 series nVidia GPUs, is unable to be auto detected by the app at this time due to the privileged access need to read this setting.
  - In the interim, a manual MFG multiplier and target MFG FPS selection will be presented on the UI when a 5000 series nVidia GPU is detected.
  - Match the app's MFG multiplier with what you have set for MFG with MSFS in nVidia settings.
  - Set to MFG Off if not using MFG or using an alternative FG method.
  - Feature can be removed by the user setting MfgModeMultEnabled to false in MSFS_AutoFPS.config in the app root directory.
- Detection of all FG types other than LSFG is automatic within 5 seconds of making the change. Detection of LSFG is normally only performed upon starting a flight. If LSFG is started after this detection is normally performed, press the Reset button for it to be detected.
- Only one type of FG can be active at a time for the app to show FPS correctly. In particular, using native nVidia or the FG mod AND LSFG will cause incorrect FPS calculations in the app because they function differently when MSFS loses focus. Choose one or the other if you want to use them with this app.

My default MSFS graphics settings are messed up and each time I try to change them back they get messed up again. How do I fix this?
- You are likely trying to change these default MSFS settings while the app is still running and you are in an active flight, where the app will override any such changes you try to make.
- Either exit the app completely or be in the MSFS main menu (ie. NOT in a flight), then you can go to the MSFS settings screen and change your default MSFS settings to what you want and the app will restore these at the conclusion of a flight session or upon exiting.

If you are not familiar with what MSFS graphics settings do, especially TLOD, OLOD and cloud quality, and don't understand the consequences of changing them, it is highly recommended you do not use this utility.

This utility is unsigned because I am a hobbyist and the cost of obtaining certification is prohibitive to me. As a result, you may get a warning message of a potentially dangerous app when you download it in a web browser like Chrome. You can either trust this download, based on feedback you can easily find on Avsim and Youtube, and run a virus scan and malware scan before you install just be sure, otherwise choose not to and not have this utility version.<br/><br/>

## Requirements

The Installer will install the following Software:
- .NET 8 Desktop Runtime (x64)
- Visual C++ Redistributable (x64)
- MobiFlight Event/WASM Module

<br/>

[Download here](https://github.com/ResetXPDR/DynamicLOD_ResetEdition/releases/latest)

(Under Assets, the DynamicLOD_ResetEdition-Installer-vXYZ.exe File)

<br/><br/>

## Installation / Update / Uninstall
Basically: Just run the Installer.<br/>

Some Notes:
- DynamicLOD_ResetEdition has to be stopped before installing.
- Mobiflight Module:
  - If the installer can't locate your Community folder to install this module, perhaps because of a Custom MSFS install location, download the latest module version from [here](https://github.com/MobiFlight/MobiFlight-WASM-Module/releases) and manually extract to your Community folder.
  - If the MobiFlight Module is not installed or outdated, MSFS also has to be stopped.
  - If you have duplicate MobiFlight Modules installed, in either your official or community folders, the app may display 0 value Sim Values and otherwise not function. Remove the duplicate versions, rerun the app installer and it should now work.
  - If the installer fails when checking/updating Mobiflight, despite the latest version being correctly installed in your MSFS Community folder, create a shortcut for the installer, add the command line option "-bypassmobiflight" to the target text box, then run the shortcut to be able to bypass this installation step.
- Do not run the Installer as Admin!
- If you wish to retain your settings for an update version, do NOT uninstall first, as that deletes all app files, including the config file. Just run the installer, select update and your settings will be retained.
- The "Clean Install" option will recreate new configuration files without having to remove the app first.
- The "Install Latest Redistributables" option will silently (other than UAC prompts) update your system with the latest Visual C++ Redistributable and .NET 8 runtime versions.
  - Mandatory for initial installations, optional for manual updates, and disabled for quick updates to avoid UAC prompts.
- If you wish to remove an Auto-Start option from a previous installation, rerun the installer and select Remove Auto-Start and the click Update.
- For Auto-Start either your FSUIPC7.ini or EXE.xml (MSFS) for the applicable MSFS versions installed is/are modified. The Installer does not create a Backup.
- The utility may be blocked by Windows Security or your AV-Scanner, try if unblocking and/or setting an Exception helps (for the whole Folder)
- The Installation-Location is fixed to %appdata%\DynamicLOD_ResetEdition (your Users AppData\Roaming Folder) and can't be changed.
  - Binary in %appdata%\DynamicLOD_ResetEdition\bin
  - Logs in %appdata%\DynamicLOD_ResetEdition\log
  - Config: %appdata%\DynamicLOD_ResetEdition\DynamicLOD_ResetEdition.config
- If after installing and running the app your simconnect always stays red, your TLOD and OLOD values show as zero or you see "Critical Exception occurred: DynamicLOD_ResetEdition - Unable to load DLL 'GpuzShMem.x64.dll' or one of its dependencies" in the log file:
  - Try reinstalling the app with the "Clean Install" and "Install Latest Redistributables" options selected. If any of the redistributables fail to install during this process, try downloading and installing/repairing (as applicable):
    - A Microsoft official version of “Microsoft Visual C++ 2015 - 2022 Redistributable”, which may be missing from your Windows installation. Try installing [this](https://aka.ms/vs/17/release/vc_redist.x86.exe) and [this](https://aka.ms/vs/17/release/vc_redist.x64.exe).
    - The NET desktop runtime from [here](https://builds.dotnet.microsoft.com/dotnet/WindowsDesktop/8.0.15/windowsdesktop-runtime-8.0.15-win-x64.exe) if still available. Alternatively, go to the Micrsoft .NET 8.0 download page [here](https://dotnet.microsoft.com/en-us/download/dotnet/8.0) and download and install the latest .NET Desktop Runtime X64 version.
  - If still not resolved and the error code in your AutoFPS log file is Exception 31, you most likely have a corrupt MSFS WASM installation.
    - First, try deleting the MSFS WASM folder, located under the Microsoft Flight Simulator directory in either %appdata% or %localappdata% for Steam and MS Store install directories respectively, which will rebuild when you next run MSFS.
    - If that doesn't fix it, a full clean reinstall of MSFS will be required, which can be done in less than 15 minutes for MSFS 2024 but may take many hours for MSFS 2020.
      - If reinstalling MSFS 2024, you need to do a **CLEAN** install, not just an uninstall/reinstall as doing the latter does not remove the likely-offending MSFS appdata folder and hence will not resolve the issue.
        - **Backup or relocate your Community folder before proceeding, and restore it after reinstallation is complete.**
        - Follow the **CLEAN** install instructions outlined for your MSFS version [here](https://flightsimulator.zendesk.com/hc/en-us/articles/17335196046108-How-to-clean-install-the-simulator-on-PC) **EXPLICITLY**. Do NOT skip the step where you manually delete the MSFS install in your user folder.
        - All your settings, controller assignments, career progression and your pilot profile are retained.
        - If you chose not to restore your Community folder, you will need to install this app again to install the required mobiflight module there.
- If you get an "Unable to attach MSFS - app disabled." message, the most likely causes are that MSFS is loading in very slowly and the attachment process is timing out, MSFS and this app are running at different permission privilege levels, or your anti-virus/malware app is blocking this app. To resolve, try the following:
  - Restart this app after MSFS has loaded in to the main menu.
  - Check that MSFS is not running as administrator.
  - Set an exclusion for this app in your anti-virus/malware app.
  - If all else fails, try running this app as administrator.
- If you get an "MSFS compatibility test failed - app disabled." message there are numerous possible causes:
  - You have started MSFS, made changes to MSFS settings and then started this app. To rectify:
    - First, try exiting this app, go to the MSFS settings menu, toggle any simple setting eg. vsync, save changes then restart this app.
    - If that doesn't work, try exiting this app and MSFS completely, start this app then start MSFS.
  - There is an issue with permissions and you may need to run the app as Administrator. 
  - You may have changed MSFS settings in your UserCfg.opt file beyond what is possible to set in the MSFS settings menu. To rectify, go into MSFS settings at the main menu and reset to default (F12) the graphics settings for both PC and VR mode, then make all changes to MSFS within the MSFS settings menu.
  - A new version of MSFS may introduce a different memory map than expected, preventing the app from auto‑adjusting to the new settings location.
    - In this case, the app will attempt to offer an auto‑update to the version most likely to be compatible. This may be a test build if no stable release is available.
    - Release‑channel users temporarily moved to a test build for compatibility will revert to release‑only updates with the next formal version (manual opt‑in to test updates remains available).
    - If no suitable auto‑update is found, or if the update does not achieve compatibility, I am likely already aware and working on a solution. However, if you may be among the first to encounter the issue (e.g. on an MSFS beta), please raise a new issue on GitHub or contribute to an existing one.
- If you get an error message saying "XML Exception: Unexpected XML declaration" or "Exception: 'System.Xml.XMlException' during AutostartExe" when trying to install with the auto-start option for MSFS, it usually means your EXE.xml file has a corrupted data structure. To resolve, copy the content of your EXE.xml into MS Copilot and ask it to check and correct it for you. Paste the fixed structure back into your EXE.xml file, save it, then try reinstalling again.
- To uninstall
  - Ensure you have completely exited the app (ie. it is not hiding still running in your SysTray),
  - Run the installer and select Remove on the first window.
  - This will remove all traces of the app, including the desktop icon, MSFS or FSUIPC autostart entries if you used them, and the entire app folder, including your configuration file.

<br/><br/>

## Usage / Configuration

- General
  - Update Management
    - **Silent Updates** install updates automatically without prompts, except for compatibility updates and reversion from test versions, which are always prompted.
      - The installer window appears briefly during the update process and release notes are shown afterwards, with no user interaction required.
      - A one‑time migration prompt is provided for existing Prompted Updates users to switch to Silent Updates.
      - Older versions of the app that don’t recognise Silent Updates will continue to treat this setting as Prompted Updates, ensuring full backward compatibility.
    - **Prompted Updates** (default) automatically install updates but seeks user confirmation for updates and displays release notes.
      - Mandatory updates will auto install regardless of user settings.
      - Optional updates will seek user confirmation and switch to **Show Updates** if declined.
      - Installer runs automatically, showing Release Notes in Notepad and auto-starting the new version.
    - **Show Updates** displays available updates and download links.
    - **Mandatory Updates Only** displays and installs only mandatory updates.
    - **+ Test** opts users into test version updates.
      - Test version users will have **+ Test** force enabled and greyed out.
      - **Mandatory Updates Only** will be unavailable until the app updates to a release version.
    - App startup sequence ensures update check is completed before connecting to MSFS.
  - Starting manually: anytime, but preferably before MSFS or in the Main Menu. The utility will stop itself when MSFS closes.  
  - Closing the Window does not close the utility, use the Context Menu of the SysTray Icon.
  - Clicking on the SysTray Icon opens the Window (again).
  - Running as Admin NOT required (BUT: It is required to be run under the same User/Elevation as MSFS).
  - Do not change TLOD, OLOD and Cloud Quality MSFS settings manually while in a flight with this app running as it will conflict with what the app is managing and they will not restore to what you set when you exit your flight. If you wish to change the defaults for these MSFS settings, you must do so either without this app running or, if it is, only while you are in the MSFS main menu (ie not in a flight).
- App Window
  - Position will be remembered between sessions, except movements to it made while in VR due to window restoration issues.
  - Will automatically reset to default position (50,50) if the app is restarted within 10 seconds of last closing.
  - Position will be saved during the session and will restore that state on next start-up.
  - Can be shown at any time by double clicking, or right-click select Show Window, on the app icon in the system tray.
- Connection Status
  - Red values indicate not connected, green is connected.
  - Automatically identifies which MSFS version is in use as either MSFS2020 or MSFS2024 and the version number.
  - If the sim version is showing in red and is not the MSFS version you wish to configure before starting that MSFS version, click the 20->24 or 24->20 button, as applicable, and it will change to that.
- Sim Values
  - Will not show valid values unless all three connections are green.
  - Red values mean FPS Adaption is active, orange means LOD stepping is active, black means steady state, n/a means not available right now.
  - When MSFS is detected and **NOT** in a flight session:
    - Default **TLOD**, **OLOD**, and **Cloud Quality** values are displayed and refresh within one second of changes made in the MSFS settings menu.
    - **VR‑specific defaults** show automatically when in VR mode.
- General
  - User Profiles:
    - You have six different Sets/Profiles for the AGL/LOD Pairs to switch between (manually but dynamically).
    - Profile list names can be edited in the app by double clicking on the profile combo box to toggle edit-ability, with non-editable being the initial state on startup.
    - When in edit mode, press Enter, press Tab or click on another control on the app UI for the changed text to be accepted.
  - Cruise LOD Updates, when checked, will continue to update LOD values based on AGL in the cruise phase, which is useful for VFR flights over undulating terrain and has an otherwise negligible impact on high level or IFR flights so it is recommended to enable this.
  - LOD Step Max, when checked, allows the utility to slow the rate of change in LOD per second, with increase and decrease being individually settable, to smooth out LOD table changes. This allows you to have large steps in your LOD tables without experiencing abrupt changes like having it disabled would do, hence it is recommended to turn it on and start out with the default steps of 5.
  - Redetect button - Redetects PC/FG/LSFG/VR graphics mode if changed by the user after commencing a flight, now necessary because the app no longer needlessly polls repetitively for graphics mode changes.
  - On Top - Allows the app to overlay your MSFS session if desired, with MSFS having the focus. Mainly useful for adjusting settings and seeing the outcome over the top of your flight as it progresses. Should also satisfy single monitor users utilising the native nVidia FG capability of MSFS as they now see the true FG FPS the app is reading when MSFS has the focus.
  - Pause when MSFS loses focus - This will stop MSFS settings being changed while you are focused on another app and not MSFS. It is particularly useful for when using native nVidia FG as the FG active and inactive frame rate can vary quite considerably and because FG is not always an exact doubling of non-FG FPS.
  - Status Message - On app start-up indicates key system messages, such as:
    - Before loading a flight - whether a newer version of the app is available to download and install
    - Loading in to a flight - whether the MSFS memory integrity test has failed, and
    - Flight is loaded
      - Shows current sim rate with a range of 0.125X to 16X, which will display at the start of the app status line for any value except 1X, detected DX version (MSFS 2020 only), Graphics Mode (PC, FG, LSFG, MFG, FSR3 or VR), and app pause or FPS settling time status as applicable.
      - The FPS settling timer runs for 6 seconds to allow FPS to settle between pausing/unpausing and PC/FG/LSFG/VR mode transitions. This allows the FPS to stabilise before engaging automatic functions and should lead to much smaller TLOD changes when seeking the target FPS on such transitions.
- LOD Level Tables
  - The first Pair with AGL 0 can not be deleted. The AGL can not be changed. Only the xLOD.
  - Additional Pairs can be added at any AGL and xLOD desired. Pairs will always be sorted by AGL.
  - Plus is Add, Minus is Remove, S is Set (Change). Remove and Set require to double-click the Pair first.
  - A Pair is selected (and the configured xLOD applied) when the current AGL is above the configured AGL. If the current AGL goes below the configured AGL, the next lower Pair will be selected.
  - A new Pair is only selected in Accordance to the VS Trend - i.e. a lower Pair won't be selected if you're actually Climbing (only the next higher)
  - Many users are finding it better to reduce, not increase, OLOD values at higher altitudes as you can't clearly see objects from such distances anyway, especially in VR.
- FPS Adaption:
  - Settings in the FPS adaption area only work if you have checked Limit LODs.
  - FPS Adaption will activate when your FPS is below the target FPS you have set, after any Delay start you have set.
  - Reduce TLOD/OLOD is the maximum values it will reduce those settings by from the current LOD pair values, minimum TLOD/OLOD permitting. If you want to use the Decrease Cloud Quality option without reducing LODs, set these both to 0.
  - Minimum TLOD/OLOD is the minimum values it will allow those settings to reduce to.
  - Delay start is how many seconds of FPS below the target FPS have to occur before FPS Adaption will activate, to stop it false triggering with a transient FPS drop. Default is 1 second but 2 seconds is good too.
  - Reduce for is how many seconds of FPS above the target FPS, plus cloud recover FPS if used, have to occur before FPS Adaption will cancel, to stop it false cancelling with a unsustained FPS increases.
  - Decrease Cloud Quality, when checked, will reduce cloud quality by one level while FPS adaption is active. 
  - Cloud Recovery FPS + is how many FPS to add to the target FPS for determining whether to cancel FPS adaption once activated. This provides an FPS buffer to account for the increased FPS achieved by reducing cloud quality to stop FPS adaption constantly toggling on and off.
- **Less is more**:
  - Fewer Increments/Decrements are better of reasonable Step-Size (roughly in the Range of 25-75) or use Step LOD Max to spread LOD changes out over time.
  - Don't overdo it with extreme low or high xLOD Values. A xLOD of 100 is reasonable fine on Ground, 200-ish is reasonable fine in the air. 400 if you have a super computer.
  - Tune your AGL/LOD Pairs to the desired Performance (which is more than just FPS).
  - FPS Adaption is just *one temporary* Adjustment on the current AGL/xLOD Pair to fight some special/rare Situations.
  - Forcing the Sim to (un)load Objects in rapid Succession defeats the Goal to reduce Stutters. It is *not* about FPS.
  - Smooth Transitions lead to smoother experiences.  
<br/><br/>
