# Bitwarden Fail2Ban config (Login Attempts)

This filter checks bitwardens `access.log` (nginx) for HTTP code `400` for the path `identity/connect/token`

### Quickstart

copy `filter.d/bitwarden.conf` to `/etc/fail2ban/filter.d/bitwarden.conf` 

add this to `/etc/fail2ban/jail.local`:

	[bitwarden]
	enabled = true
	filter = bitwarden
	logpath = /path/to/your/bwdata/logs/nginx/access.log
	chain = DOCKER-USER
	maxretry = 5
	bantime = 1h
	port = 8080,8443

adjust `maxretry` and `bantime`

test with `sudo fail2ban-regex /path/to/your/bwdata/logs/nginx/access.log /etc/fail2ban/filter.d/bitwarden`
