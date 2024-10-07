
oc cp frontend-1-zvjhb:/var/log/httpd/error_log \
    /tmp/frontend-server.log

oc rsh frontend-1-zvjhb ps ax

oc rsh -t frontend-1-zvjhb              --> Interactive Shell