# Obsidian.md-1.8.4-Privacy-Forensic-Analysis
# Table of Contents

- [Concept](#Concept)
- [Overview](#Overview)
- [Testing](#Testing)
- [Analysis](#Analysis)
- [References](#References)

---



<h2>#Concept</h2>
<h3>What is <a href="https://obsidian.md">Obsidian</a>?:</h3> 
Privacy Focused Note taking application
<h3>What is it used for?:</h3>

| Notes, Journaling, Research, Brainstorming and Visualization. | ![homepage](https://obsidian.md/images/screenshot-1.0-hero-combo.png) |
|-|-|

<h3>What does Obsidian marketed for?: </h3>

| <ol><li>Privacy focused</li><ul><li>No one else can read them.</li><li>Entirely stored offline</li></ul><li>Quick, Easy Access</li><li>Heavily Customizable</li></ol> | ![options](./Images/MarketedOptions.png) |
|-|-|

<h3>What do they provide?: </h3>

| <div width="500"><ol><li>Links between notes</li><li>PinBoard-Like Visualizer Graph for Interactive Ideas</li><li>Canvas for diagramming and brainstorming ideas</li><li>Thousands of User Created Plugins</li><li>Standardized non-proprietarily readable file types .md</li><li>Paid-for service</li><ul><li>Syncing notes across devices</li><li>End to end encryption</li><li>Collaboration on shared vaults</li><li>Publishing</li><li>Easy ability to Publish notes to web</li></ul></ol></div> | <img src="https://obsidian.md/images/sync-settings.png" width="600" /> |
|-|-|

<h3>How did I learn about this tool?: </h3>

| <div>While researching during college I became addicted to using the "red twine on pin board" technic, and I actively researched something akin to that to use their Windows and Linux versions on PC for note taking.</div> | <img src="./Images/web.png" width="1000" /> |
|-----------------|-----------------|

<h5><a href="https://obsidian.md/download">DownloadLink</a></h5>
<h5>The images provided were from the <a href="https://obsidian.md">Obsidian.md</a> webiste</h5>

<hr>
<br><br><br>
<h2>#Overview</h2> 

| I will be focusing on gathering information involving internet connection to confirm if Obsidian.md is a good choice for privacy-concerned individuals. I will be focusing on finding all files found on the local system, the permissions in the apk file, database information when it concerns the web and modules utilized within the actual application to see if they are problematic. |
|-|



<hr>
<br><br><br>

<h2>#Testing</h2>
I preformed two acquisitions of data:
The first Acquisition of a physical, rooted Pixel 3 Phone to get the before and after installation and utilization of the applciation, Full File System (ls -alR /):
This was done to get a starting point to any and all changes that the Obsidian.md application makes within the file system.

The second acquisition was of the same rooted Pixel 3 Android V.13 Phone to re-perform similar tasks done in the second acquisition, although this time only looking for information that pretained to Obsidian.md. This was done with 5 minute intervals and the following timed script.

<h3>Acquistion 1 Actions in Order:</h3>

| **Time/Date**|**Action Taken**|
|-|-|
| 19:07 EDT 04/06/2025|Turn On Phone|
| 19:10 EDT 04/06/2025|Unlock Phone|
| 19:35 EDT 04/06/2025|Install APP through ADB|
| 19:36 EDT 04/06/2025|Open APP|
| 19:36 EDT 04/06/2025|Grant Access to Managing all file permission|
| 19:36 EDT 04/06/2025|Name:Vault1, location: Documents, and Create Vault|
| 19:37 EDT 04/06/2025|New Note named V1|
| 19:37 EDT 04/06/2025|Add [[V2]] to V1|
| 19:38 EDT 04/06/2025|Click on [[V2]] to create new note named V2|
| 19:39 EDT 04/06/2025|Create a Folder named Folder|
| 19:39 EDT 04/06/2025|New Note in Folder named V3|
| 19:40 EDT 04/06/2025|Add [[V1]] to V3|
| 19:40 EDT 04/06/2025|New Note in Folder named V4|
| 19:41 EDT 04/06/2025|Screenshot the File Explorer|
| 19:42 EDT 04/06/2025|Insert Screenshot to V1|
| 19:44 EDT 04/06/2025| Close Application |
| 19:45 EDT 04/06/2025| Force Stop Application from running in background in app settings |


<h3>Acquistion 2 Actions in Order:</h3>

| **Time/Date**|**Action Taken**|
|-|-|
| 22:00 EDT 05/04/2025|Turn On Phone|
| 22:05 EDT 05/04/2025|Unlock Phone|
| 22:10 EDT 05/04/2025|Install APP through ADB|
| 22:15 EDT 05/04/2025|Open APP|
| 22:20 EDT 05/04/2025|Grant Access to Managing all file permission|
| 22:25 EDT 05/04/2025|Name:ObsidianVault, location: Documents, and Create Vault|
| 22:30 EDT 05/04/2025|New Note|
| 22:35 EDT 05/04/2025|Title: Note1 Info: Lorem ipsum|
| 22:40 EDT 05/04/2025|Add [[Note2]] to Note1|
| 22:45 EDT 05/04/2025|Click on [[Note2]] to create new note named Note2|
| 22:50 EDT 05/04/2025|Add Ipsum lorem to Note2|
| 22:55 EDT 05/04/2025|Create a Folder named ObsFolder1|
| 23:00 EDT 05/04/2025|Drag Note2 into ObsFolder1|
| 23:05 EDT 05/04/2025|Screenshot the screen|
| 23:10 EDT 05/04/2025|Insert Screenshot to Note2|
| 23:15 EDT 05/04/2025 | Close Application |
| 23:20 EDT 05/04/2025 | Force Stop Application from running in background in app settings |

Now that we know where to look, we can now extract these artifacts and parse through the data!
| Location: | Why is this important? |
|-|-|
| /data/app/~~J4PHE12PKyRx8lrqqstftQ==/md.obsidian-LV_ft233GdUFJTmDP_6PRA==/base.apk | The installed application apk file |
| /data/data/md.obsidian/app_webview/Default/ | Databases, Cookies, the leveldb file and Web Data |
| /sdcard/Documents/ObsidianVault/ | The actual md files and directories made from Obsidian.md |


<hr>
<br><br><br>

<h2>#Analysis</h2>
Here is what I found!
<!--what did i do specifically to gather the information and stuff-->
<h3>/sdcard/Documents/ObsidianVault/</h3>
Within this directory are the following files:

```
ls -alR /sdcard/Documents/ObsidianVault
/sdcard/Documents/ObsidianVault:
total 66
drwxrwx--- 2 root everybody  3452 2025-05-04 22:25 .obsidian
-rw-rw---- 1 root everybody    22 2025-05-04 22:40 Note1.md
drwxrwx--- 2 root everybody  3452 2025-05-04 23:00 ObsFolder1
-rw-rw---- 1 root everybody 56530 2025-05-04 23:10 Screenshot_20250504-230510.png

/sdcard/Documents/ObsidianVault/.obsidian:
total 16
-rw-rw---- 1 root everybody    2 2025-05-04 22:25 app.json
-rw-rw---- 1 root everybody    2 2025-05-04 22:25 appearance.json
-rw-rw---- 1 root everybody  636 2025-05-04 22:25 core-plugins.json
-rw-rw---- 1 root everybody 3884 2025-05-04 23:10 workspace-mobile.json

/sdcard/Documents/ObsidianVault/ObsFolder1:
total 4
-rw-rw---- 1 root everybody 47 2025-05-04 23:10 Note2.md
```
|Purpose|Code|
|-|-|
|**app.json**: empty but based on context should be basic extra application configuration options |```{}```|
|**appearance.json**: empty but based on context should be extra appearance configuration options |```{}```|
|**core-plugins.json**: .obsidian houses the Obsidian Plugin Settings|```{"file-explorer": true,"global-search": true,"switcher": true, "graph": true, "backlink": true, "canvas": true, "outgoing-link": true, "tag-pane": true, "properties": false, "page-preview": true, "daily-notes": true, "templates": true, "note-composer": true, "command-palette": true, "slash-command": false, "editor-status": true, "bookmarks": true, "markdown-importer": false, "zk-prefixer": false, "random-note": false, "outline": true, "word-count": true, "slides": false, "audio-recorder": false, "workspaces": false, "file-recovery": true, "publish": false, "sync": true}```|
|**workspace-mobile.json**: The json map of the connections/organization of the notes| <img src="./Images/workspace-mobile.png" width="400" /> |
|**Note1.md**: The first note we made|```Lorem ipsum```<br>```[[Note2]] ```|
|**Note2.md**: The second note we made and put into ObsFolder1|``` Ipsum lorem```<br>```![[Screenshot_20250504-230510.png]] ```|
|**Screenshot_20250504-230510.png**: A copy of the screenshot we attached to Note2.md| <img src="./Images/Screenshot_20250504-230510.png" width="300"/>|

<h3>.../base.apk</h3>
There are many artifacts within this apk file, which is a duplicate of the original Obsidian.md apk file.

|Items of Note|Purpose|
|-|-|
| **AndroidManifest.xml** |Defines permissions within the application: <br>android.permission.INTERNET<br>android.permission.READ_EXTERNAL_STORAGE<br>android.permission.WRITE_EXTERNAL_STORAGE<br>android.permission.MANAGE_EXTERNAL_STORAGE<br>android.permission.RECORD_AUDIO<br>android.permission.MODIFY_AUDIO_SETTINGS<br>android.permission.VIBRATE|
|**classes.dex**| Houses the Java Code and packages involved:<br>getcapacitor (allows for the ability to use HTML/CSS/JS files and run them natively<br>helps Obsidian call and store data with json files)|

*(These were opened using jadx-gui for Windows)*

<h3>/md.obsidian/app_webview/Default/</h3>
Shows no data being stored within the databases involving Web Data nor Cookies. There was nothing of note within the filled "meta" tables.

|Items of Note|Purpose|
|-|-|
|Databases.db|Only table with values within is the "meta" data table. Nothing under "Databases" or "sqlite_sequence".|
|QuotaManager|Only table with values within is the "meta" data table.<br>Under "buckets":```storage_key:http://localhost/	host:localhost	type:0	name:default	use_count3	last_accessed:13390885526734038	last_modified:13390888219954324```|
|Cookies|Only table with values within is the "meta" data table. Nothing under "cookies".|
|Web Data|Every table is empty besides "meta"<br><img src="./Images/webdata.png" />|
|-|-|
|-|-|

*(Used DB Browser for SQLite to open the database files)*

<h3>apk2url</h3>
apk2url pulls string values from within all of the files of base.apk looking for exclusively mentioned urls and ip addresses.

|Items of Note|Purpose|
|-|-|
|Obsidian.md Links|To be expected there are many links from the App back to the Obsidian website.|
|IPs to other countries|There was an issue with the script where due to the end of Javascript file having a large amount of numbers separated by ".", there is a large list of "not actual ip address".|
|Example Domains|"www.example.com", these are not to be concerned of and are never called, mentioned within comments.|
|Module Script Domains|To be expected, module and library scripts will have links back to where they came from.|
|<img src="./Images/url1.png" />|<img src="./Images/url2.png" />|

<img src="./Images/notrealchineseipaddress.png" />

<hr>
<br><br><br>

<h2>#References</h2>
<li>Tools Used: Andriller, ADB, Magisk, apktool, jadx-gui, apk2url, DB Browser for SQLite, grep, ls, powershell</li>
<li>Jacobs, J. (2025, January 20). Reverse Engineering Chinese Social Media for Fun (REDNote App). Medium. <a href="https://infosecwriteups.com/reverse-engineering-chinese-social-media-for-fun-rednote-app-4c9871006c6c">https://infosecwriteups.com/reverse-engineering-chinese-social-media-for-fun-rednote-app-4c9871006c6c</a></li>
(Thank you Jason Jacobs, MSc., with your rednote reverse engineering it introduced me to a couple tools that helped me complete this project!)


