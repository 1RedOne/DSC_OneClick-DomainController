<a href="http://foxdeploy.com/learning-dsc-series/"><img class="alignnone wp-image-2172 size-large" src="https://foxdeploy.files.wordpress.com/2015/03/introtodsc.jpg?w=705" alt="IntroToDsc" width="705" height="154" /></a>

<span style="color: #666699;"><strong>This post is part of the Learning PowerShell DSC Series, here on FoxDeploy. Click the banner to return to the series jump page!</strong></span>

<hr />

I've been pointing people here for a while now, and noticed that my instructions were not 100% accurate, plus I was sending people all over the web to download the needed files to build a Domain Controller using DSC.  So, in this post, I'll provide much simpler instructions to deploying a one-click domain controller.

* First and foremost,<a href="https://github.com/1RedOne/DSC_OneClick-DomainController"> download a .zip of the full repo here </a>
* Now, make sure you have a Windows Server machine ready, running WMF 5.0.  If you need it, <A href="https://www.microsoft.com/en-us/download/details.aspx?id=48729">download it here</a>
* Next, extract this to your new Domain Controller to be, under C:\temp.
* Copy all of the x$ModuleName folders into `$env:ProgramFiles\WindowsPowerShell\Modules` on your VM
* From an Administrative PowerShell prompt, run: `dir -recurse -path $env:ProgramFiles\WindowsPowerShell\Modules | Unblock-File` to unblock all files downloaded

Now, simply launch OneClickDSC.ps1 in PowerShell, and click the Play button (or hit F5), to launch the GUI

<img class="alignnone wp-image-2172 size-large" src="https://raw.githubusercontent.com/1RedOne/DSC_OneClick-DomainController/master/postImg/DSCPrompt.png" alt="IntroToDsc"/>


Now, type in the password of the first domain admin to be created.


<img class="alignnone wp-image-2172 size-large" src="https://raw.githubusercontent.com/1RedOne/DSC_OneClick-DomainController/master/postImg/DomainAdminCreds.png" alt="IntroToDsc"/>

First step for application, is to change the computer's name.  This requires a reboot.  So...reboot.

<img class="alignnone wp-image-2172 size-large" src="https://raw.githubusercontent.com/1RedOne/DSC_OneClick-DomainController/master/postImg/RebootToChangeTheName.png" alt="IntroToDsc"/>


On restart, we can run the following commands to watch the rest of the DSC Application
#Pause the last application
Stop-DSCConfiguration -Force
#Resume so we can watch it
Start-DscConfiguration -ComputerName localhost -Wait -Force -Verbose -UseExisting

You may run into an error, specifically w/ the computername module.  I'm not sure what the issue here, as the system seems to be renamed, but you can safely ignore it. 

And...we're done when we see this screen!

So, not a lot of meat to this one, but I hope this clears up the questions people were asking about how to use this 'OneClick Domain Controller'
