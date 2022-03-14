# wildcard-SSL
wildcard-SSL cert server custom config'd


vi /etc/nginx/conf.d/map-wp-fastcgi-cache.conf

#map $request_uri $uri_no_cache {
#    default 0;

    "~*/.*" 1;
 
nginx -t && systemctl reload nginx

**ssl-rsync.sh

#!/bin/bash
rsync --exclude *.csr --exclude *.key --exclude *.conf --ignore-existing /etc/letsencrypt/renewal/kln.ac.lk/ /var/www/ssl.ict.kln.ac.lk/htdocs/

**ssl-acme.sh 

#!/bin/bash
.acme.sh/acme.sh _{--issue/--renew}_ \
-d kln.ac.lk \
-d *.kln.ac.lk \
-d *.news.kln.ac.lk \
-d *.library.kln.ac.lk \
-d *.fcms.kln.ac.lk \
-d *.science.kln.ac.lk \
-d *.ss.kln.ac.lk \
-d *.fct.kln.ac.lk \
-d *.hu.kln.ac.lk \
-d *.units.kln.ac.lk \
-d *.administration.kln.ac.lk \
-d *.journals.kln.ac.lk \
-d *.nelrc.kln.ac.lk \
-d *.cdce.kln.ac.lk \
-d *.iccms.kln.ac.lk \
-d *.staff.kln.ac.lk \
-d *.pgiar.kln.ac.lk \
-d *.pgipbs.kln.ac.lk \
-d *.conf.kln.ac.lk \
-d *.ict.kln.ac.lk \
-d *.fgs.kln.ac.lk \
-d *.medicine.kln.ac.lk \
-d *.ghrusa.kln.ac.lk \
--dns dns_cf --force

crontab -e

37 0 * * * "/etc/letsencrypt"/acme.sh --cron --home "/etc/letsencrypt" --config-home "/etc/letsencrypt/config" > /dev/null

0 0 * * 0 /opt/cf-update.sh > /dev/null 2>&1 # Cloudflare IP refresh cronjob added by WordOps

_**37 0 * * * /path/ssl-rsync.sh > /dev/null 2>&1 # rsync sslcert to web root by me**_

