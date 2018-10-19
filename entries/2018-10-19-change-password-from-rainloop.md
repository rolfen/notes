# Change your password from Rainloop

You may have set up a mailserver on Debian using the (previously mentioned) [great guide from Thomas Leister](https://thomas-leister.de/en/mailserver-debian-stretch/).

Would you like to let users change their passwords? [rainloop](https://rainloop.com) webmail has a [custom sql password change](https://github.com/RainLoop/rainloop-webmail/tree/master/plugins/change-password-custom-sql) plugin.

Follow the README instructions to copy the plugin to the data directory, and the plugin shows up in the rainloop admin, under 'Plugins'.

Enable it by clicking on the checkmark next to it, then click on the plugin name to configure it.

You get a popup where you should enter the MySQL host, user, password, database, table and statement.

If you have (like me) forgotten the MySQL password (or something else), `grep` can do the trick:

```
$ sudo grep -r dbname /etc/dovecot/ 
/etc/dovecot/dovecot-sql.conf:connect = "host=127.0.0.1 dbname=vmail user=myUser password=myPass"
```

If you followed the tutorial, the table name should be `accounts`.


The SQL statement is:

```
UPDATE `:table` SET `password`=ENCRYPT(':newpass', CONCAT('{SHA512-CRYPT}$6$',sha(RAND()))) WHERE `username`=':username' AND `domain`=':domain' AND `password`=ENCRYPT(':oldpass', password)

```

## Testing and Troubleshooting

To test it, log into webmail as a user, go to settings, there should be a new "Password" page. Try changing your password.

If you get a "Could not save new password" error, then have a look at rainloop logs, which are buried in the rainloop data directory.
For example, if today is 19 October 2018, then launch:

```
tail -f data/_data_/_default_/logs/log-2018-10-19.txt
```
Try to change your password and watch the output of `tail`.

## Forgotten Password

If you want to reset your password, you can either use the method in [the setup guide](https://thomas-leister.de/en/mailserver-debian-stretch/#create-a-new-user-account) or you can do it in a single SQL query (replace `myUsername`, `myDomain` and `myPassword`) :

```
UPDATE `accounts` set `password`=ENCRYPT('myPassword', CONCAT('{SHA512-CRYPT}$6$',sha(RAND()))) WHERE `username`='myUsername' AND `domain`='myDomain';
```

## (Potential) Issues

The methods above create password values which are not prepended with '{SHA512-CRYPT}', as opposed to the [`doveadm pw` method](https://thomas-leister.de/en/mailserver-debian-stretch/#create-a-new-user-account).
It seems to work, but I don't have a deep understanding of the procedure, so maybe some further research and testing would be good, to rule out any edge cases and potential issues.

There is a concern about escaping - single quotes in the "new password" input (in rainloop) are not properly escaped, they cause an SQL syntax error, this has to be further investigated.
