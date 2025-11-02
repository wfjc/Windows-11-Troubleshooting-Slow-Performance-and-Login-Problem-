



<h1> Windows-11-Troubleshooting-Slow-Performance-and-Login-Problem </h1>

<h2>Description</h2>
Project consists troubleshooting and resolving issue of user (Clive) trying to logon and having slow performance and error messages
<br />


<h2>Languages and Utilities Used</h2>

- <b>File Explorer</b> 
- <b>Windows Settings</b>
- <b>Event Viewer</b>
- <b>Bitlocker</b>

<h2>Environments Used </h2>

- <b>Windows 11</b> (21H2)

<h2>Project run through:</h2>

<p align="center">
So I start off simulating sluggishness by opening lots of apps and files to get memory up high : <br/>
<img src="https://i.postimg.cc/BZCC0d6n/1-Simulating-problem-A-make-system-slow.png" height="80%" width="80%" alt="Open command ready drive"/>

  We could resolve this by obviously closing any apps and things like what I have opened here on Clive's account, but also by configuring which processes open on startup using startup tab.
<br />
<br />
I log out of Clive and into William C the administrator to simulate a 'corrupted profile' by changing Clives user folder name from 'Standard_Clive' to 'Standard_Clive.old'.. this should cause a login error  <br/>
<img src="https://i.postimg.cc/nV11J6zF/2-renaming-clive-to-simulate-problem.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />


I logged off Will C the administrator account and back into Standard_Clive user to see if the 'corruption' was achieved. Success.  <br/>
<img src="https://i.postimg.cc/kMyymk45/3-corrupted-Clive-profile.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

I again sign out from corrupted clive profile and into the William C administrator account to try to resolve the issue. I decided to make a new Clive account under Windows Settings, Accounts, Other Users. Here I am just filling out new account information for 'New Clive'  <br/>
<img src="https://i.postimg.cc/nV11J6zV/4-Creating-new-Clive.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
So, here I am now copying these files of the original Clive (corrupted one) and will copy to the New_Clive account's documents under Users.  <br/>
<img src="https://i.postimg.cc/HWttgfx8/5-copying-files-from-corrupted-clive-to-new-clive.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
To check the corruption and login problems were resolved, I logged into New Clive account from William C administrator and the error message disappeared.
At that point I tried to practice more with event viewer and tried to find any logs relating to log on errors. I filtered the search using 'Winlogon' and 'User Profile General' under Event Sources, Application, Windows Logs. <br/>
<img src="https://i.postimg.cc/SQGGhws2/6-using-event-viewer-checking-logs.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Under recommendations online I am looking for error codes like '1500 profile cannot be loaded' or '1502 Windows cannot load the locally stored profile' or '4625 Failed logon attempt', but I only found 6000 or 6003 which are WinLogon and User Profile Service as that's what I filtered for. The others are under security logs which I learned that I need to activate Auditing policies to view. .  <br/>
<img src="https://i.postimg.cc/7PNNkp6T/7-finding-error-codes-in-Winlogon.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Just to understand further, I wanted to see the auditing policies, so I researched how to view auditing logs. I ran 'secpol.msc' which opened Local Security policy. In security settings I found Auditing policy under local policies.
I then double clicked 'Audit Logon Events' and 'Audit Account Logon Events' to which I ticked success/failure to show these events in Event Viewer like discussed previously. I then restarted to lets changes take effect. <br/>
<img src="https://i.postimg.cc/4ybHT7Tf/8-Enabling-logon-auditing.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Back in Event Viewer now, I filtered the current logs to show security logs like 4624 and 4625. I also set the time for last 12 hrs to further narrow down results. So I have used Event Viewer here to see any problems that could match what the user is describing in troubleshooting.   <br/>
<img src="https://i.postimg.cc/prY5thtX/9-Checking-Security-Logs-Filtering-searches.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
It's actually very enjoyable/satisfying to try and turn theory into practical experience in homelabs... From this project I have tried to learn how to troubleshoot problem logins and followed steps to resolve the issue by removing programs on startup through TaskManager, migrating the corrupted account to a fresh one and utilised Event Viewer to try and see any error codes relating to the profile problems for reference.
I used AI and online resources to help me understand, but I tested the results myself in a lab to grasp these concepts better. My goal was to show real troubleshooting practice, not just memorisation.
