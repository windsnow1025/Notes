# Tips Entry

- Checkbox: ☑

- Google Takeout
  - Deselect: Google Drive, YouTube and YouTube Music - videos

- Adobe disable Recent Files
  - Preferences >> File Handling >> Recent File List Contains: 0

- Adobe Premiere Pro preview glich
  - RightClick Preview Window >> Enable `High Quality Playback`

- Spotify delete Local File Resources
  - Delte Spotify folder in `C:\Users\{username}\AppData\Local\Packages`

- Enable Intel graphic card in Asus motherboard
  - BIOS >> Advanced >> Graphics Configuration >> iGPU Multi-Monitor >> Enabled

- Microsoft Edge managed by your organization
  - Registry Editor >> HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft >> Delete Edge folder

## Windows
- Hyper-V boot loader failed
  - Hold down a key when starting up the virtual machine

- Hyper-V windows login problem
  - View >> Untick `Enhanced session`
  - Settings >> Accounts >> Sign-in options >> Untick `For improved security, only allow ...`
  - View >> Tick `Enhanced session`

- EXE crashes immediately upon launch without error message displayed.
  - Use CMD to directly open the executable file by entering its path

- RDP: This user account's password has expired
  - Win + R >> lusrmgr.msc >> users >> <account_name> >> disable "User must change password at next logon", enable "Password never expires"

- Change device name, alert: A connection with the name you specified already exists
  - Download [https://github.com/jschicht/RunAsTI](https://github.com/jschicht/RunAsTI) to open CMD as TrustedInstaller
  - `CMD > regedit`
  - `Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\NetworkSetup2\Interfaces\`
  - `IfAlias` property in `.\[Id]\Kernal\ifAlias` represents the name
  - Find the conflict one and delete its [Id] folder

- Snipping Tool Screenshot brightness error for HDR
  - Snipping TOol -> Settings -> HDR screenshot color corrector

- Permanently Remove Disk Data: `cipher /w:<driver_letter>`

## Microsoft 365

- Microsoft Excel change default font
  - File >> Options >> Language >> Office authoring languages and proofing >> Remove `Chinese (Simplified)`

- Microsoft Onenote fix Quick Notes language
  - Delete `%HOMEPATH%\AppData\Local\Microsoft\OneNote`

### Microsoft Word

- Change default font
  - `Design` >> `Fonts` >> `Office: Aptos Display` >> `Set as Default`

- All new documents opened in Compatibility Mode
  - `%HOMEPATH%\AppData\Roaming\Microsoft\Templates` >> Open `Normal.dotm` >> `File` >> `Info` >> `Compatibility Mode`: `Convert` >> `Save`

- Disable Auto Selection
  - `File` >> `Options` >> `Advanced` >> `Editing Options` >> Uncheck `When selecting, automatically select entire word`

- Precise ruler
  - Hold `Alt` when dragging the ruler

- Format formula copied from Wikipedia
  - Delete `\displaystyle` >> `Alt` + `+`
    - Equation: LaTeX
    - Convert: Current - Professional

- Allow English Text Wrap
  - Paragraph >> Asian Typography >> Allow Latin text to wrap in the middle of a word

## Android Debug

### ADB

1. Install Android Studio
2. Settings >> Languages & Frameworks >> Android SDK
3. Add platform-tools to environment variables
4. SDK Tools >> Install Google USB Driver

### Fully uninstall App

1. Check package names: `adb shell cmd package list packages -u`
2. Reinstall package: `adb shell cmd package install-existing <package_name>`
3. Permenantly uninstall package: `adb shell pm uninstall <package_name>`
