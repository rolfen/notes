## Sending an SMS using mmcli

When I plug my Android phone into my Linux Desktop, I can see a GSM modem device appearing. I can use that to get 4G on my computer. I had seen an article about sending SMS on Linux, and have been wanting to try this.

I will try to use `mmcli` which appears to me as a modern, user friendly and mainstream option.

This article outlines the procudure:

https://itgrenade.wordpress.com/2016/09/14/use-mmcli-for-sending-sms/

So basically:

List modems. Take note of modem # to use in the next command:

	mmcli -L

Create an SMS on modem # 0. Take note of the SMS # in the output:

	sudo mmcli -m 0 --messaging-create-sms="text='Hello world',number='+1234567890'"

Send SMS # 0:

	sudo mmcli -s 0 --send

This worked.


## Receiving

Then I tried to receive an SMS, however Android gets a hold of them and they never make it to ModemManager. 

However, given a dedicated GSM modem, this works pretty well:

	mmcli -m 0 --messaging-list-sms

Then for example, read SMS number 15;

	mmcli -s 15
	
	
## Etc.

Check your mobile internet usage (Alfa Lebanon):

	mmcli -m 0 --3gpp-ussd-initiate='*11#'
	
## GUI

There is pretty nice GUI for sending and receiving SMSes (and some other nice functions):

https://bitbucket.org/linuxonly/modem-manager-gui/src/default/

However the version that was provided by Debian packages had a fatal bug - I had to compile from source using the linke above. It was worth it!
