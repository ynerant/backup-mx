# backup-mx
Simple postfix backup mailserver for your Docker containers. Based on Alpine Linux.

## Description

This image allows you to run POSTFIX internally inside your docker installation.

## TL;DR

To run the container, do the following:
```
docker run --rm --name backup-mx -e "HOSTNAME=mx2.example.com" -e "DOMAINS=example.com,example2.com" -e "RELAYHOST=mx1.example.com" -p 25:25 -v "./postfix-spool:/var/spool/postfix" ynerant/backup-mx
```

## Configuration options

The following configuration options are available:
```
ENV vars
$HOSTNAME = Postfix myhostname
$DOMAINS = Domains for relaying
$RELAYHOST = The nexthop SMTP server where postponed mails are delivered
```

The `/var/spool/postfix` should be secured in a volume to avoid losing some mails.

### `DOMAINS`

Postfix will try to deliver emails asap to the primary server, defined in `$RELAYHOST`.

## Security

Postfix will run the master proces as `root`, because that's how it's designed. Subprocesses will run under the `postfix` account
which will use `UID:GID` of `100:101`.
