StreamEngine Origin
1) apt-get update & apt-get upgrade
2) apt install docker.io
3) build directories under root (will change), conf/custom.conf 
4) `listen              1935;
max_connections     1000;
srs_log_tank        file;
srs_log_file        ./objs/srs.log;
daemon              off;
http_api {
    enabled         on;
    listen          1985;
}
http_server {
    enabled         on;
    listen          8080;
    dir             ./objs/nginx/html;
}
stats {
    network         0;
    disk            sda sdb xvda xvdb;
}
vhost __defaultVhost__ {
    forward {
           enabled on;
           destination 45.33.127.44:19350;
       }
}
`
5) `docker run -p 1935:1935 -p 1985:1985 -p 8080:8080 \
    -v /root/srs/conf/custom.conf:/usr/local/srs/conf/srs.conf \
    -v /root/srs/log/srs.log:/usr/local/srs/objs/srs.log \
    ossrs/srs:3`
