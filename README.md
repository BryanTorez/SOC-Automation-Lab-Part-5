<h1>SOC Automation (Home Lab) - Part 5</h1>

<p align="center">
<img src="https://snipboard.io/KsE1Zf.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<h2>Description</h2>
<br />
<p align="center">
Welcome to the final part of the series of the SOC automation project. If you haven't seen the previous parts where we go over on how to build out a diagram for this lab, install, configure, and generate telemetry, I highly recommend you go and read that first to get up to speed.
<br />
<br />
<img src="https://snipboard.io/jeyGl4.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
In today's objective, it's going to be about connecting both our Shuffle, which is our SOAR platform. Which will then send an alert over to the Hive and to our analyst, such as yourself via an email to begin your work.
<br />
<br />
<img src="https://snipboard.io/l8XYqM.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
By the end of this part, you will have a fully functional lab that integrates Wazuh, the Hive, and Shuffle. Now, Wazuh alone does have a lot of these capabilities built-in, however, it is a good idea to be exposed to how we can utilize SOAR and a case management system like the Hive. You want to stick around to the end because, I'll be introducing a relatively new tool that had helped me during my investigations. 
<br />
<br />
<br />
<br />
So you want to head over to Shuffle's site at "Shuffle.io" and then you want to create an account. Once you create an account, we can start creating our workflow. Now you'll be presented with this screen. Once you log in, we can either select "New to Shuffle" or "Experienced", but either way I'll just bypass everything and click on "Workflows".
<br />
<br />
<img src="https://snipboard.io/RSiCdb.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
From here, we can open up and create our own workflow by clicking on the plus button. I'll name this workflow as "SOC Automation Project" and the description will be "MyDFIR Project!". 
<br />
<br />
<img src="https://snipboard.io/t26KyN.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/GilLSQ.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/scdQIU.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
For the Usecase, we can do whichever. I'll just select any random one and then hit "Done". We get presented with this big "Change Me" icon. Now, this is your workplace where you get to start adding apps and triggers.
<br />
<br />
<img src="https://snipboard.io/LqhM7z.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/3RyepB.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
On the bottom there is a tab in the middle called "Triggers" and that is what we want to click on. Now, we are presented with a couple of workflow starters. So there's "webhook", a scheduler, "Office365", and "Gmail". I'm going to select "webhook". Simply just drag and drop it. Once you've dragged and dropped the webhook, you want to select it and then on the right-hand side we can start naming our webhook to whatever we want to.
<br />
<br />
<img src="https://snipboard.io/EyjBMK.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/MZIAO5.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/aptuLT.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
In our demo, I'll name this as "Wazuh-Alerts". For the "Find Associated App", it is optional so I'll leave it as blank. What I want to do is copy the webhook URI. The reason we copy this webhook is because we'll need to add this into our "ossec" configuration posted on our Wazuh manager.
<br />
<br />
<img src="https://snipboard.io/ZRUFS2.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
However, before we head over to the Wazuh manager, let's click on the "Change Me" icon and just make sure that it is selected as "Repeat back to me". For the call, I'll remove "Hello world" and I'll click on this plus button. Select "Execution Argument" and then I'll save it now.
<br />
<br />
<img src="https://snipboard.io/5CVJUz.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/8obQ4x.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Let's head over to our Wazuh manager. On our Wazuh manager CLI, we need to tell Wazuh that we're going to connect to Shuffle and we can do this by adding what is called an Integration Tag in the "ossec" configuration file. So let's go ahead and open that up. 
<br />
<br />
<br />
<br />
If you don't remember, it is under "/var/ossec/etc/ossec.conf". From here, I'm just going to scroll down just a little bit right after the "global" tag. Now, you could place this anywhere you like but I'm just going to place it here. Then, I'm going to copy and paste this integration tag similar to the other configuration files.
<br />
<br />
<img src="https://snipboard.io/SIbR6N.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/0uTGUE.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/oXYubl.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/ZjibUK.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
You do want to keep in mind of the indentation. If you don't know how many spaces there are, just look above and try to match it so it's the same. Now, that the integration tag is there, we want to replace the URL where it says your "SHUFFLE_URL". Let's go ahead and remove all of that, including the "HOOK_ID". Then, paste in the webhook that you copied earlier.
<br />
<br />
<img src="https://snipboard.io/9fUBXQ.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/y21jRA.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
After you pasted in your Shuffle webhook, you want to make sure that your "hook_url" is not included as the URL. So you want to press space in between to make sure that your "hook_url" is white and not purple because if it is purple, it'll think that it's related to the Shuffle URL. As a side note, if I press "Space" it separates it from the URL itself. That is what we want to do.
<br />
<br />
<img src="https://snipboard.io/ozyt9N.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/7N8CpT.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, by default it has a level of three. So this means that any alert that has a level of three will be sent to Shuffle. Now, I personally don't want this and instead I want only our "rule_id" that we created, which was '100,002' and that was our Mimikats rule that we created earlier.
<br />
<br />
<img src="https://snipboard.io/QBtqzg.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Again, if we wanted to send all alerts that were generated with a level of three or whatever the number is, we need to change the number to reflect that level. However, because I want a "rule_id" instead of a level number, I will change the level tag to "rule_id" tag.
<br />
<br />
<br />
<br />
So for example, again just to make sure that we are all on the same page. If I wanted to send all level five alerts to Shuffle, I will need to change it from '3' to '5'. In my case, because I don't want level and I want "rule_id", I will remove the level and type in "rule_id".
<br />
<br />
<img src="https://snipboard.io/jqpeLB.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/K42Xvr.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Then I'll change my '5' to '100,002'. Make sure you close it off correctly by typing in "rule_id". So this looks good. Our indentation is good to go. My "hook_url" is not attached to the URL itself and my "rule_id" is '100,002'. I'll go ahead and save this out.
<br />
<br />
<img src="https://snipboard.io/pXPJt1.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/Pb10sW.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Remember, if we make any changes to our configuration, you want to restart your Wazuh manager service. Once that is restarted, let's just make sure it's good to go. So we'll type in, "systemctl status wazuh-manager service".
<br />
<br />
<img src="https://snipboard.io/EGzw8c.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/8Z4OsP.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Let's go and regenerate the Mimikats telemetry on our Windows client machine. So I have my Powershell here. I'll exit out of that and then type in ".\youareawesome.exe". Hit "Enter". Now, let's head over to our Shuffle instance.
<br />
<br />
<img src="https://snipboard.io/GCJuAg.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/8DzAJp.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Click on our webhook and make sure you select "Start". Now let's click on the person icon at the bottom. As this will show us any executions. So we'll click on that and let's go and test workflow. Now that is extremely strange, there is no events pushing over to my Shuffle.
<br />
<br />
<img src="https://snipboard.io/HVM8Ud.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/FOtZ3p.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/UN5Vo4.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/Ve3AkY.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So let's do a little bit of troubleshooting, shall we? We'll go back to our Wazuh manager and we'll open up the configuration file. Now, I just need to make sure to read my URL or anything such as my "rule_id" I do recall seeing that it's '102' which is correct, but if you look at the URL there's "HTTP" and "https" so that is clearly wrong. We will remove "HTTP" and save that out. Now that should be good. 
<br />
<br />
<img src="https://snipboard.io/2jmgpa.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/EyZKJG.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/ClZeOj.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Let's restart Wazuh manager. Now that's done, let's head back over to our client machine. Exit out of Mimikatz. I'm going to clear the screen because it's getting quite messy and then type in ".\youareawesome.exe".
<br />
<br />
<img src="https://snipboard.io/T7s04R.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/R3g8Xe.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now we should see some events in Shuffle. Now let's go ahead and click on the Wazuh alert. Select the "Execution Argument," and expand that. Look at that, we get all of the information that was generated from Wazuh itself. Isn't that awesome? Think about all the possibilities that we can do.
<br />
<br />
<img src="https://snipboard.io/sTMOtx.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/KJNfY7.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/dhY4rD.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
The workflow that we will build for Mimikatz today will only work for this demo, but the same concepts can be applied to other use cases. As long as you follow the guidelines and read the instructions, you should be good to customize your own alerts and automation.
<br />
<br />
<br />
<br />
Here is the workflow that we will be creating today. We will have our Mimikatz alert be sent over to Shuffle, Shuffle will then take that and extract the file hash from the file, and then check the reputation score using VirusTotal. We will then send that over to the Hive to create an alert and then we will send an email to the analyst so they can perform further investigation.
<br />
<br />
<img src="https://snipboard.io/OTYulv.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
When we look at our return values for the hashes, we notice that its appended by their hash type. For example, in this case it is appended by "SHA1=" and then the hash value. If we wanted to automate this, we would need to parse out the hash value itself, because the entire value including the "SHA1=" will be sent over to, let's say VirusTotal, to check and we don't want to do that, we just want to send VirusTotal the hash value. Why don't we actually do that? So let's close this out. 
<br />
<br />
<img src="https://snipboard.io/4ZFegp.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
I'll click on the "Change Me" icon and instead of "Repeat back to me", we actually have a couple of other options that we can use. So we can type in "regex" and select Rexgex capture group.
<br />
<br />
<img src="https://snipboard.io/m1cg7i.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/Xsh6Kt.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
For the input data, we can select the plus button and select "Execution Argument" and let's look for our hash. Now if you highlight over it, you'll actually get the values or the output on the left-hand side.
<br />
<br />
<img src="https://snipboard.io/aPJXDz.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/WDH8qU.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now at the bottom, it tells us to do some rexgex. Do you know how to write regex by any chance? If not, that is perfectly fine. We can head over to our trusty ChatGPT. Using ChatGPT, we can create a prompt saying "create a regex to parse the sha256 value of the hash" and then I'll hit "Enter".
<br />
<br />
<img src="https://snipboard.io/E80Qov.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Right off the bat, ChatGBT created a regex for us. So we can start copying that. Once it's finished talking, I'll scroll back up to copy the regex and then I'll head over to Shuffle. Now, we can paste in the regex that ChatGBT created for us and use AI to our advantage in these types of cases.
<br />
<br />
<img src="https://snipboard.io/HfCu2W.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/gHBJyC.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/voTYNt.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Once we pasted that in, let's save our workflow and then we can click on the person icon. Then, click on the refresh button or rerun workflow button at the top. We'll click on that and then if we were to expand our results, we can see that it parsed out the sha256 hash. Now, when we encounter something that we aren't too familiar with, don't be afraid to utilize ChatGPT and ask it to help you.
<br />
<br />
<img src="https://snipboard.io/0wqU38.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/N4t2gA.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/vTf38Q.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
We can utilize AI to our advantage to allow us to become better at what we do. Now, that you have parsed the hash value for the file, we can automatically send that over to VirusTotal and check the reputation score. Now, I will rename "Change Me" to "SHA256_Regex".
<br />
<br />
<img src="https://snipboard.io/X6arjC.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/i9LIyl.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
The next thing we want to do is utilize VirusTotal's API. That that way we can automatically ask VirusTotal to check this hash and return the values to us. In order to utilize their API, we must create an account with them. So let's go and do that.
<br />
<br />
<img src="https://snipboard.io/vOBoZA.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
You can head over to VirusTotal's site and then click on "Sign up" on the top-right corner. Once you've created your account, go ahead and copy your API key and then head back over to Shuffle. Once we're in Shuffle, we can click on "Apps" and then we want to search for VirusTotal and hit "Enter".
<br />
<br />
<img src="https://snipboard.io/B5zXDt.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, we can click on VirusTotal and then it will activate VirusTotal onto our Shuffle instance. Once that's done, go ahead and drag VirusTotal over and it will automatically connect. Now, when you click on VirusTotal, rename it as "Virustotal".
<br />
<br />
<img src="https://snipboard.io/S2dUWH.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/jIT1Rq.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/SOzP2N.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/q3Z1MU.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
For "Find Actions", I don't want an IP address. Instead, I want to look for a hash. So I'll click on the drop-down. Now, you might only see one action. That's okay, that's simply because VirusTotal is still activating in the background. You want to wait just a bit and then more actions will populate.
<br />
<br />
<img src="https://snipboard.io/L1Stb0.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So it's been a couple minutes and I went ahead and refreshed my Shuffle instance. Now, when I click on VirusTotal under the "Find Actions", I can see more actions. Again, I'm not looking for an IP address report. Instead, I want to look for the hash. So I'll type in "hash", and I can find that there's a hash report.
<br />
<br />
<img src="https://snipboard.io/f2xNbr.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/9CGQzl.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
If you want, you can paste in your API key here or you can authenticate with "VirusTotal V3". By clicking on "AUTHENTICATE VIRUSTOTAL V3", I'll paste in my API key that I copied from Virustotal. Then, I'll hit "Submit".
<br />
<br />
<img src="https://snipboard.io/pwIZ9l.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/9daCWl.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Make sure for the hash section, to select the regex output. Right now, it's pointing to "$exec.all_fields.agent.ip" and we don't want that. We want to select the regex output for "list". Since again, the rexgex is there to parse out the value of the hash. Now, I'll go ahead and save the workflow.
<br />
<br />
<img src="https://snipboard.io/1fx37B.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/nCpQDY.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/WkDwgZ.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/OKLM8W.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Click on the person icon and then we'll select the middle workflow option. Then, we'll rerun workflow. Now let's take a look at VirusTotal's output. We'll go ahead and expand that and we notice that the status is '404'. So that is quite strange. This means that VirusTotal was not able to return any results for us.
<br />
<br />
<img src="https://snipboard.io/hOT5L8.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/G1ujsf.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/QPTXuU.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/fqj8Cz.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, if we were to look at the query itself in the URL section. We see that it's going to "api/v3/files/report" and then we see our "hash=" the hash value. So this seems about right, but how come it's giving us a '404' error?
<br />
<br />
<img src="https://snipboard.io/uJe9f8.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Let's head over to VirusTotal's API documentation. If I were to scroll down we see that there is a "Get a file report by hash" and that is what we're interested in. So I'll go ahead and click on that and I want you to take a look at the URL here.
<br />
<br />
<img src="https://snipboard.io/bkMaJ1.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/tHXNZL.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/qI4AX6.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
It is going to "api/v3/files/{id} and that's interesting. So if we were to go back into our Shuffle. Our URL is going to "/api/V3/files/report". The documentation mentioned nothing about "report". So maybe that is why we are getting a '404' error. The VirusTotal app in Shuffle has an incorrect URL or it was probably correct before but VirusTotal updated its API.
<br />
<br />
<img src="https://snipboard.io/bBEZ79.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, how do we fix this? We can actually head over to VirusTotal's app and edit it. So to do that, let's head over to apps. Once you are in the application page, you want to select the new window under the VirusTotal app. You'll be presented with VirusTotal's application page for Shuffle. What you want to do is "Fork" over the application so you can edit it. So let's click on that. 
<br />
<br />
<img src="https://snipboard.io/8MrSLQ.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/0cP5gk.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/V5LeSs.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/kMoN7K.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Scroll down and then let's find our hash report. Now, we can see that it is indeed referencing "report". As you recall looking at API documentation on VirusTotal, it did not mention anything about "report". Instead, it was pointing towards an ID variable enclosed in curly brackets.
<br />
<br />
<img src="https://snipboard.io/6qcLFS.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/HlM95R.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So that's what I'll do. I'll change that and then hit "Submit". I'll scroll down and save it out. Let's try this again. I've placed the edited VirusTotal onto our workflow so I'll go ahead and select that. Again, you do have an option to authenticate with the API key or you can click on the plus icon to authenticate. I will be using the API key, so I'll paste in my VirusTotal API key and hit "Submit".
<br />
<br />
<img src="https://snipboard.io/L6eVyZ.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/eliVMz.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/2qN6sw.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/Qrlf1X.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, I do not want to get an IP address report. Change this to "Get a hash report". Change the ID to the regex ID. Then, we'll go ahead and save the workflow and rerun it. 
<br />
<br />
<img src="https://snipboard.io/JNEYSr.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/qDhW0U.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/PeMdJR.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/aT8Ajg.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Click on "Rerun" and let's expand VirusTotal. Look at that, it's a lot different. If we scroll down to "last_analysis_stats". We can see that it says "malicious : 63". That means that '63' scanners had detected this file as malicious. Now, you might be asking how did I know which field to use or the reputation, and that's a great question. When I search our hash through VirusTotal, we can see that it detects '63' out of '72'.
<br />
<br />
<img src="https://snipboard.io/8hL2Qa.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/xfTdze.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/4evOdm.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/oS9aOV.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
All we need to do now is grab the output that Shuffle had provided us and search for '63'. So we obtained the field name, which in our case was malicious under the last analysis stats, which sounds about right. To quickly recap, we set up our SOAR platform to receive our Wazuh alert. We then performed regex to parse out the sha256 hash, and we then used VirusTotal to check its reputation.
<br />
<br />
<img src="https://snipboard.io/pLWPzy.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Next, we will send the details over to the Hive. So the Hive can create an alert for case management. So under the "Application" tab at the bottom left-hand corner, we want to search for The Hive and we want "TheHive 5". So click on that and then we will drag it over to our workflow and then let's take a look at the action.
<br />
<br />
<img src="https://snipboard.io/hst6pU.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/805uSK.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, we might again see only one action, but that's okay. It's since loading in the background. If you don't want to wait, you can try refreshing your workflow to see if theHive's actions will populate. So I went ahead and refreshed my workflow and I do see a lot more actions.
<br />
<br />
<img src="https://snipboard.io/vk5Eoc.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Before we move on with Shuffle, let's head over to TheHive. If you recall, we can log in using the default credentials of "admin@thehive.local" and the password is "secret". By default, we only have one organization and that is named "admin". Let's create a new organization and create a new user for that organization.
<br />
<br />
<img src="https://snipboard.io/gahzer.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/6stCc5.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
To do that you want to click on the plus button at the top-left corner. For the organization name, I'll just name this "Mydfir" and the description will be "SOC Automation Project". I'll confirm that. Now, that we have a new organization, go ahead and click into it. Immediately, it says no users have been found. So let's add two users.
<br />
<br />
<img src="https://snipboard.io/ERA5Lt.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/URp1QM.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/WnYxFN.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/QWEF3R.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
For the first user, I'll leave the type as "Normal" and the login will be "mydfir@test.com". For profile, I'm going to select "analyst". I'll save. For the second user, instead of selecting "Normal", I'm going to select "Service". In this case. For the login, I'll type in "shuffle@test.com" and the name I'll just type in "SOAR".
<br />
<br />
<img src="https://snipboard.io/xQ0WO5.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/vhFP4c.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
As for the profile, we're going to select "analyst". In a real world environment, you would want to create a new set of permissions with the principle of lease privilege in mind and tie that to the service account. The principle of lease privilege, for those that don't know, is where an account is given the minimum level of permission to perform its function. In our case again, because it is a demo environment, we're okay to just select "analyst". I'll hit "Confirm". 
<br />
<br />
<img src="https://snipboard.io/fCh6HA.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
The next thing we want to do is create a password for the "mydfir" account. We can highlight the account and select "Preview". Scroll down and then you will see "Set a new password".
<br />
<br />
<img src="https://snipboard.io/ENXgBm.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/daiPlL.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Once you set a password, hit "Confirm". For the SOAR user, you want to select "Preview" and you want to create an API key for this user. Once your API key is created, go ahead and copy that out and make sure you put it somewhere safe because we will be using this to authenticate with Shuffle.
<br />
<br />
<img src="https://snipboard.io/eLvcR8.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/aI1F0o.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/hUtXKa.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, I'll log out of this administrative account and then I will log into "mydfir" account. Once you log in, you're now presented with a different page. We can see cases, well, in this case hahaha, no cases have been found. However, we'll see cases here eventually, and you'll also see alerts.
<br />
<br />
<img src="https://snipboard.io/ibT9jI.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/Y0K59V.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/g3CWOB.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, let's head over to Shuffle and configure that to work with The Hive on our Shuffle instance. We want to select the plus button beside "Authenticate" because we want to authenticate to The Hive using our API key. Copy the API key and paste it into your Hive. As for for the URL, you want to type in the public IP of your Hive instance, along with the port number.
<br />
<br />
<img src="https://snipboard.io/ZbQ8Do.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/lOrhS0.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
 Great. Now under the "Find Action", I don't want to query the API. Instead, I want to create an alert. So I'll select "Create alert" and at the bottom we need to select is the "Date".
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, to get the date we must connect our Hive to the workflow. So I'll connect VirusTotal to The Hive. That way, it can take a look into our Wazuh alert. So to select the date, I'll click on the plus button and then I'll click on "Execution Argument".
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, before I even go through that, I want to show you what it looks like without the connection. So if click on the "Date" and select the plus button, I don't see anything. Well, I see something but I don't see VirusTotal. Now, I do want to connect it so I can see how it flows.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
I'll select "Date" and hit the plus button. Now I can see "Sha256" and "Virusotal" as well. It just seems a lot cleaner to me, so that's why I like to make sure I connect things. Now, we'll go into "Execution Argument". Then, we'll look for "utcTime".
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, if you're not sure. Again, if you just highlight the field, it will populate the field value on the left-hand side. I'll select "utcTime". For the description, let's type in "Mimikatz Detected on host:" and let's select the field name that contains the host.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So we'll add on "from user:". Let's scroll down, to find "user". So if I were to receive an alert, what are some of the fields that will provide a lot of information? Now, this is very subjective depending on the analyst itself. However, for the sake of this demo, I'll just leave it as these two for now.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
For external link, we don't need to add anything for now. For the flag, we'll put it as false. As for the value, two is the default, according to the documentation. "Pap" is permissible actions protocol, aka the level of exposure of information.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Next is severity, which I will put it as two. For the source, typically this is where the alert is coming from. I'll just say "Wazuh". The source reference is just a little bit of metadata for the alert itself. I'll just put in "Rule: 100002".
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
The "Status" is the status of the alert that will be created in the Hive. So we want the "Status" to be new. For the summary, similar to the description, I'll type in "Mimikats activity detected on host:". Let's select "Computer". For the process ID, this is all up to you on what kind of information you want it to spit out.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Essentially, I'm going to ask it for the process ID and the command line. Search and click on "commandline". Awesome. Now you can keep building this, but again for the sake of the demo, I'll just leave it as is. For the tags, we need to put this into an array.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
I'll put in the Mitre Attack tag. Which is "t1003", AKA credential dumping. For the title, I'll type in "Mimikats Detected". Now, this is very static. What we can do is just tie it to the alert itself. "Tlp" is the traffic light protocol, so the confidentiality of information.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
I'll leave it as '2'. For the type, I'll type "internal", as in where did that alert come from. Now, let's go ahead and save this workflow. However, before we run the workflow. We'll need to modify our cloud firewall to allow all IPS's coming inbound on Port '9000'.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Since that is where my Hive instance will live. This will be a temporary rule to allow us to test this automation. So let's head over to our Digital Ocean and click on "Networking". Head over to our "Firewalls". Then, select the firewall that we created.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, we want to create a new rule and put it as custom. Then, we want to add in the port '9,000'. We will remove "All IPv6", but we will keep all "IPv4". I'll save it out. Now, any source will have access to our machines on Port '9000'. 
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Heading back to our Shuffle. We can now rerun the workflow. So click on the person icon and then rerun the workflow. Scrolling down, it looks like the Hive was successful. So let's go into our Hive instance. Look at that, automatically the alert was created.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
"Mimikats Usage Detected". Click on that and we have our description and summary. Now, you can see how powerful this is if you really put in more effort into the summary and description because this will tell the analyst a bunch of information very quickly.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
The next step is to send an email to our analyst containing relevant information. To do that, you can click on "Apps" at the bottom left and drag the email application. Then, connect VirusTotal over to the email. Now, we can enter in the recipient, so I can type in any email I want, as long it is a valid email.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, if you don't want to use your personal email. Well I want to introduce you to our SquareX. Not only do they offer disposable email, they also have what are called disposable web browsers and file viewers. I'll enter in my disposable email from SquareX and now let's change the information to provide some details.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
The subject will be "Mimikats Detected!". Then, I'll put in "time:". Let's head over to our execution arguments and then let's look for "utcTime". Type in "title:". I think it's useful to put in the computer name as well, right?
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
If Mimikats is detected, you want to know where it was detected from. Wonderful, let's go ahead and save that out. Now, we'll rerun the workflow. Heading over to my disposable email from SquareX, we can click on the new email that was received.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Look at that, "Shuffle - Mimikats Detected!" That is super cool. To showcase the responsive feature, I deployed another virtual machine since from my testing it seems that the responsive scripts for Windows don't work as well compared to Linux.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
I will use a similar workflow, however this time, we will add a user input. Then, we'll ask the user if they want to block a certain IP. Now, I did not show you the steps for creating an Ubuntu virtual machine and configuring some of the options since I want that to be your lab portion, but I will demonstrate the responsive action.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Our goal here is to block any source IPS that attempts to connect to our Ubuntu machine, via SSH. To do this, you will need to have your Ubuntu machine in the cloud and create a rule to allow all TCP connections towards this Ubuntu machine. However, you can do this On-Prem and use an attacker machine that you own to simulate a SSH brute force attack.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
In Shuffle, we want to add on the HTTP application. So I'll go ahead and drag that over. I'll rename this as "Get-API" and have defined action as "Curl". For the statement, at the bottom you want to include the following and make sure that a firewall rule exists to allow all inbound traffic to Wazuh on Port '55,000'.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, the reason that we are doing this is because if we want to utilize Wazuh's API capability, we must first authenticate and obtain a JWT token, AKA a JSON web token. In order to do that, we need to initiate a "curl" with a username and password.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, if you recall, there was a Wazuh API user. That is the user account that we'll be using. Now Shuffle will be making this request, so that is why we need to make sure that port is opened for all IP addresses. Now once you created your firewall rule to allow traffic inbound to Port '55,000', we can now look for Wazuh's application.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So let's go ahead and search that and then click it to start downloading and activating it. Once you have Wazuh activated, you can go ahead and drag and drop it onto your workflow. Now, I do have to mention when you click on the "Get-API", do remember to fill in the user and password for the Wazuh API account and include your Wazuh IP here.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
If you leave it as default, it's not going to work. So I'll just go ahead and change this right now. I'll save the workflow. Now that's good, we'll head over to the Wazuh application. I'll leave "Find Actions" as "Run command". As for the API key, we'll select our "Get-API" at node.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So if I were to rebuild this workflow just a little bit, this is how it will look like. The Wazuh alert will feed into the "Get-API". The "Get-API" will then feed over to VirusTotal. VirusTotal will run its reputation on the source IP and then VirusTotal will eventually connect to what is called a User Input.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
That will ask the user if they want to block that IP. Now, I don't want to put in the user input yet, so I'll just connect VirusTotal over to Wazuh. That way we can test the responsive capability without constantly asking the user to see if they want to block an IP.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, that we have Wazuh connected. Again, the API key we're going to select it as "Get-API". For the URL, change the "localhost" to your Wazuh public IP. Mine is '159.203.17.39' on Port '55,000'. If we scroll down, we see what is called an Agent List. Each Wazuh agent will have an associated ID with it.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
To find this, we can head back over to Wazuh's dashboard. you want to click on the drop-down arrow and select "Agents". As we can see at the bottom, the Ubuntu agent ID is '002'. Yours might be different depending on how many hosts you have, but that is how you identify your ID.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, we can also find this ID in our sample log or alert if we head over to Shuffle. Click on our "Execution Arguments". Click on our person icon. Then, if we were to expand our "Execution Arguments". Scroll all the way down until you find a section called agent.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
There's an ID. In my case, the ID is '001' for this Windows machine. So as an agents list, I can either type it in manually or I can select it to make it dynamic. I'll click "Execution Arguments". Scroll all the way down until I see my agent ID.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
I will set the "Wait for complete" to true. Now we have "Alert", "Arguments", "Command" and "Custom". However, before we move on to the next couple of fields, we must configure active response on our Wazuh manager. Let's head over to our manager console.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
On our manager console, we want to open up the "osesc" configuration file. Scroll down to the bottom and eventually, you'll find what is called "Active response". Now, we can always hold down cntrl+w and type in "Active Response". So under active response, there are some pre-built response options that we will be using and if you take a look there are tags called "command".
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So here there's a command called "disable-account". The next command is "restart-Wazuh". There's one called "firewall-drop" and many more. These commands are essentially what you invoke. In other words, if something bad happens then do these commands.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
The most important thing here is that we want to keep keep in mind of the name itself. So in my example, I'll be using "firewall-drop". This command will modify the IP tables of our Ubuntu machine, essentially dropping all traffic to it or to the IP.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
We will now need to create an active response tag and make sure that the command reflects the command name that we want to use. For example, let me scroll down until there's no more commands and right here. We see that the active response options here. I'll remove the comment section and then I'll type in" command".
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So what is the name of the command that I want to run it is called "firewall-drop", then I want to close out the command tag. Next is the location tag, I'll put this as "local" and then close that out. Now what "local" means is that the host that generated the alert is where the script will be ran.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So for example, on my Ubuntu machine if there was a malicious IP hitting my Ubuntu machine, that is where the script is going to be executed. Next is "level", so which is the level of the alert. If you recall when we were configuring our Shuffle integration, instead of using the "level" we used "rule_id".
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
In this case, for our active response. I'm not going to be using "rule_id", instead I'm going to be using "level". I'll close out that tag. Finally, we need to type in "timeout". Now, we have our active response, so let's go ahead and save this out.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
We'll restart the Wazuh manager. We can restart it by typing "systemctl restart wazuh-manager". There is one important thing to keep in mind if you use active response, especially when it comes to API's, it's that the command name appends the timeout to the name, but it is hidden.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
I'll explain. Currently, our command name was set to "firewall-drop". However, if we want to use this via an API. We must append our timeout option to it, but there is a hidden timeout field. So my timeout was zero, so now it will append a zero in front of "firewall-drop".
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, how would you know that? One way to see the name and test to see if your script is active, is to use what is called an Agent Control Binary. This is located under "var/ossec/bin". So let's change our directory there. Type in "ls" and we can see "agent_control". That is the binary that we want.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So I'll type in "agent_control" and without any options. That way we can see what kind of options it provides. At the bottom, you can see there's a "-L". This list available active responses. So let's go and use that. Now, you can see the response name "firewall_drop0". That is the name we need to use, if we want to utilize the API.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So for example, just to make sure everything is crystal clear, if you set a timeout option say '600' seconds. That means your firewall or command name will be "firewall-drop600", and you can always verify using "./agent_control -L". To test out your active response actions, we can run "./agent_control -b".
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Then, we'll block the IP address of '8.8.8.8' which is Google's DNS. Then, we'll specify "-f" for the active response command. Now our command was "firewall-drop" and because we're using agent control, we need to specify the zero. Next I'll specify the "-u" and that is for the agent ID. Finally, I'll specify '002' and that is my Ubuntu machine.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, before I execute this active response, let's head over to my Ubuntu machine and ping '8.8.8.8' just to make sure. We can see that it's successful, so let's head back over to our Wazuh. From here, we'll go ahead and execute our active response. Now, it says "Running active response 'firewall-drop' on: 002".Let's head back over to our Ubuntu machine.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
We see that it stopped, I guess it works. So let me go ahead and cancel this out and then we'll type in "iptables --list". Then, we'll see that it's dropping DNS Google responses. We can take a look at our active response log on our Ubuntu machine to see if the active response was successful.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
This can be found under "/var/ossec/logs". Type in "ls" since we want to look for active responses. So we can go ahead and cat out active responses and we can see that there are some responses here that was successful. You can see that our '8.8.8.8' was here.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
On our Shuffle instance, let's add in the command "firewall-drop0". Scroll down on our Wazuh application, so we can find "Command" to type "firewall-drop0". Next, put in the arguments of '['8.8.8.8']'. Now, I'll save this out and then I'll rerun the workflow.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Let's head down to Wazuh and expand that out. It says "AR command was sent to all agents"... Interesting. I only sent it to number two, but that's okay. So that looks like it's been successful. Let's go and take a look at our Ubuntu machine. On the machine, I'll clear this out and then type in "cat active-responsees.log".
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, immediately I see an error that says "Cannot read source IP from data". So we know for a fact that it did not work. Now, just above it we do see our log. We see that the extra arguments our IP is listed in there and it cannot read our source IP from the data, but if you recall we did use agent control to execute our active response to test it out.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, if we look at the parameters. I know it's kind of hard to read with the parameters, but says "extra_args" is blank. There's no data for the alert that is where the source IP lives. If you look at the log that Shuffle had sent over, there is nothing in the alert itself.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So that tells me that our IP needs to be in the alert section. However, just to be safe I'm going to copy everything from the alert, up to the second curly bracket. So I'll go ahead and save that out and copy. I'll head over to our Shuffle instance.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
On our Shuffle, we want to scroll down and remove "Aguments". In the "Alert" section, let's go ahead and paste in our data. Now, let's go ahead and try that. I'll save this out and then we'll rerun the execution. However, before I run that, let's set up another ping towards '8.8.8.8' on our Ubuntu machine, just in case it does work.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So I'll set out another ping and head back over to our Shuffle. Now, we'll rerun our workflow. Let's scroll all the way down and select our Wazuh. Again, it does say an "AR command was sent to all agents". So it should be successful if our command was correctly done.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Let's head over to our Ubuntu and look at that. I'll exit out of this and then I'll take a look at our IP table list. It's there! "dns.Google", perfect. Let me go ahead and remove this by typing "iptables --flush". So we know for a fact that our Shuffle is sending an active response over to Wazuh and Wazuh is instructing Ubuntu to actually perform that command.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now the next step is to set up a user input, that way it will send an email to our SOC analyst providing all of that information. If the analyst says to go ahead and block it, Wazuh should instruct Ubuntu to block that IP.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So the only thing that we need to do is remove this chain or that link. Then, we'll go under triggers and we want to drag over "User_input_1". I'll connect VirusTotal over to the "User_input_1". Here I'll make sure that the email is selected and I'll use my trusty disposable email from SquareX because I don't want to use my email.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
For the sake of the demo, we can just say "Would you like to block this source IP:" and what is the source IP? We can just click on this plus icon and then look at the "Execution Arguments". So here's the source IP that we're interested in.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So I'll highlight this and then I'll copy it. I'll remove it and then head over to the "User_input_1". Then, I'll paste in the variable. Now, if you're following along you might be like, "What the heck did I just do?" Going back, I was just using VirusTotals query input to take a look at what the variable for the source IP was.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So in order to do that, I just clicked on the plus button, looked at the execution argument, and then I tried to find out where the source IP was. It was located at the bottom and if I didn't know for sure, I looked at the value that was presented to me on the left. So I clicked on Source IP and then I just took the variable here. Copied it.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Removed it since I don't want VirusTotal to take a look at it. Instead, I added it over to our "User_input_1". So in theory, if this workflow ran, it would ask the user if they would like to block this Source IP and it will also present the source IP to the the analyst.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
If the analyst said yes, I want to block that Source IP, the responsive feature should kick in. So let's go ahead and connect that over to our Wazuh. Make sure our Command is all good to go. Now, the source IP is no longer going to be a static IP.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Instead, I'm going to remove that and then I will select the plus icon. Select "Execution Argument". Scroll down to source IP and then I'll select that. I noticed that the variable is outside of the bracket, so I'll remove that. Then, I'll put it in between the quotes.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now that looks a lot better and a lot cleaner. I'll go ahead and save this workflow out, and now it's the moment of truth. I'm going to take a look at what the source IP is. In this case, the source IP is '103.180.149.26'. I'm going to go ahead and ping out that IP.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Hopefully, it'll accept my ping. Perfect. Let's hope our SOAR workflow works. Under our workflow, we'll rerun the workflow. So once we run it, it should go out and grab the API key for Wazuh. Then, it will enrich the data, in this case with IP. Afterwards, it will send an email to our analyst and depending on its response, it should activate a responce of action.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Let's head over to our disposable email. Click on "inbox" and let's refresh this. We have an email here that says "Would you like to block the source IP '103.180.149.26'. If this is TRUE click this..." In other words, if you want to block it, access this link. So let's try it out. 
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Let's go ahead and do that. It'll say "Would you like to block this source IP:" and it automatically selects continue for me. So the next thing to do now is head over to our Ubuntu machine and see if our active response kicked in. Since, there's just way too many going on. I'll go ahead and exit that out.
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Then I'll type in my IP tables. Let's list it out. So now our IP of '103.180.149.26' has been added to our IP tables. Our active response actions kicked in. 
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
From here, the sky is the limit and it is up to your imagination on what you want to do with this automation. Perhaps, you want to automatically reset an account from an active directory if a user entered their credentials onto a fishing page or maybe you want to contain a host if there was suspicious activity, such as our Mimikats example. Automation is something to really think about as this is the direction that we're heading towards. Now again, I did not go through the last portion in detail intentionally, because I want you to get some hands-on experience and try it out yourself. 
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now here's your homework, you want to create a Ubuntu machine in the cloud with the lowest minimum specs, so 1 gig and 25 hard drive space. You want to make sure you use a password generator so it is not easy to guess. This machine should allow all traffic inbound, meaning all sources will have access to your Ubuntu machine. You want to install a Wazuh agent onto that Ubuntu machine. Then, immediately you should see multiple failed SSH attempt alerts. Push all level five alerts to Shuffle and perform IP enrichment using VirusTotal. Send the details via email to the user, asking if the user wants to block the IP and automatically create an alert in the Hive. If the user selects "yes" to block, the IP should automatically be placed in IP tables. 
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
I hope you enjoyed it as much as I did making it. Please share this GitHub page to other aspiring analysts, so they can get some hands-on experience as well. Thank you so much for reading. Remember to stay curious and do things differently.
