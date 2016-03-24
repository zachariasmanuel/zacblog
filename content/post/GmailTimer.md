+++
date = "2014-10-14T00:29:19+05:30"
title = "Set receiving timer for Gmail incoming mails.."

+++
Sometimes, receiving mails continuously can be such a pain. If you are facing this problem, and if you are a Gmail user, be happy to know that it is possible to adjust Gmail to let in the incoming mail at a specified time. You can pause the inbox to block the mails coming to your inbox.

1\. Go to your Gmail inbox, Go to Settings and go to the tab named "labels".

2\. Under the labels tab, create a new label with the name "For processing"

![timer1][1]

3\. Go to the tab filters in Settings page and click on "create a new filter".

4\. In this page enter "*" in the "From" text box; click on "create filter with this search" and confirm creating the filter.

![timer2][2]

5\. In this you have to mark "Skip the inbox" and "Apply the label : .For processing". And click on "Create filter".

![timer3][3]

6\. After completing this go to Google Drive, click on "Create" and then go to "Script". If you are not able to find "Script" here, goto "Connect more apps", search for "script" and connect with Google Drive. Then the option "Script" will appear on this list.

![timer4][4]

7\. It will lead to a page. Now select 'Blank Project' from this page.

8\. After renaming the project remove the existing code and copy paste this code:



     
    function moveToInbox() {    
    	var threadArray = GmailApp.getUserLabelByName(".For processing").getThreads();
     	// GmailApp.markThreadRead(threadArray);
     	GmailApp.moveThreadsToInbox(threadArray);
     	var label = GmailApp.getUserLabelByName(".For processing");  
		for (var i=0; i< threadArray.length; i++) { 
    		threadArray[i].markUnread();
     		threadArray[i].removeLabel(label);
    	}
    }


9\. Before setting the timer we need to test the code. For that click on the "Run" button and confirm the authorization.

![timer5][5]

10\. If it shows an error, please check the code once again.

11\. After the successful run we need to set the timer to move mails from ".For processing" to Inbox. For that we need to set up a timer to run this code.

For setting up the timer, click on Triggers button and "Click here to add new trigger".

![timer6][6]

12\. If you want to get your mails on every morning please set the option according to the image and click on Save. You can go through the options available and customize the timer according to your needs.

![timer7][7]

13\. Now the emails will only come to your inbox on every day at 7am. If you have a urgency you can go to the label 'For Processing' and all the pending mails would be there.

GitHub link : [Here][8]

[1]: /img/timer1.jpg
[2]: /img/timer2.jpg
[3]: /img/timer3.jpg
[4]: /img/timer4.jpg
[5]: /img/timer5.jpg
[6]: /img/timer6.jpg
[7]: /img/timer7.jpg
[8]: https://github.com/zachariasmanuel/Move-to-Inbox-on-a-Schedule

