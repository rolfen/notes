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

Then I tried to receive an SMS on the computer, but it seems that Android gets a hold of them and they never make it to Linux. I guess I'll need a dedicated GSM modem for this.


