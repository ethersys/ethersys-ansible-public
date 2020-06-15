# Mailhog

Mailhog is a SMTP server useful for testing https://github.com/mailhog/MailHog

* approximative size: 13MB
* default SMTP port: 1032
* default UI pour: 8032
* default Mailhog version: 1.0.0

## Usage

To known your local adress run command (using SSH)

```bash
echo $LOCALSERVER
```

Set your app to deliver mail using SMTP on your local address and Mailhog SMTP port instead of your default SMTP settings.  
If you use a PHP app, you could configure **sendmail_path** to use **mhsendmail** for sending mail.

```bash
sendmail_path='/home/<acount_name>/bin/mhsendmail  --smtp-addr="<local_address>:<mailhog_port>"'
```

To configure access to Mailhog UI, you could create a new **User program** site with this settings (recommended way):

* **Command** : `~/bin/mailhog -auth-file $HOME/mailhog/.htpasswd -maildir-path $HOME/mailhog/data/ -storage maildir -smtp-bind-addr $IP:1032 -ui-bind-addr $IP:$PORT -api-bind-addr $IP:$PORT`
* **Working directory** : `mailhog`
* **Environment** : ``

Mailhog password file can be changed using:

```bash
htpasswd -nbB <USER> <PASS> > $HOME/mailhog/.htpasswd
```

Or you could create a new redirect site using the following settings

* type: redirect
* destination URL: http://<LOCAL_ADDRESS>:8032
* forwading type: transparent (reverse proxy)
