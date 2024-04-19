# smtp2tg
SMTP 2 Telegram very simple relay

# Building
Building tested on go version go1.22.2.

Build
```
go mod init smtp2tg
go mod tidy
go build
```

# Running
Copy binary file to /usr/local/bin, or just run from building directory:

```
./smtp2tg
```
or
```
./smtp2tg -c /etc/smtp2tg.toml
```
If you want to listen 25 port, you need run program as root.


# Daemonizing
Unfortunately, golang has some problems with daemonizing: https://github.com/golang/go/issues/227

You can "daemonize" smtp2tg with system tools, like start-stop-daemon


# Usage
You need to point valid dns MX-record to ipaddr, on which daemon is listening.
Example, if smtp2tg is listening on 1.2.3.4:
```
$ORIGIN example.com.
...
alert                   A           1.2.3.4
alert                   IN MX 10    alert.example.com.
```
And then just send email to user@alert.example.com
