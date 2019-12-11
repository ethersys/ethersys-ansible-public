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

* **Command** : `~/bin/mailhog -auth-file $HOME/.mailhog_htpasswd -maildir-path $HOME/mailhog/ -storage maildir -smtp-bind-addr $ALWAYSDATA_HTTPD_IP:1032 -ui-bind-addr $ALWAYSDATA_HTTPD_IP:$ALWAYSDATA_HTTPD_PORT -api-bind-addr $ALWAYSDATA_HTTPD_IP:$ALWAYSDATA_HTTPD_PORT`
* **Working directory** : `mailhog`
* **Environment** : ``

Mailhog password file can be created using:

```bash
htpasswd -nbB <USER> <PASS>
```

Or you could create a new transparent redirect (reverse proxy) site or a proxy (example with auth below) into **Advanced Settings** box of an Apache standard site.

```conf
ProxyPreserveHost On
ProxyPass /mail/ http://<local_address>:<mailhog_port>/
ProxyPassReverse /mail/ http://<local_address>:<mailhog_port>/

<Location /mail>
Order Deny,allow
Deny From All

AuthType Basic
AuthName "Restricted"
AuthUserFile "/home/<acount_name>/.htpasswd"
Require valid-user
Satisfy any
</Location>
```