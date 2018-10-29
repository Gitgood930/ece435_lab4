FROM ubuntu:18.04
EXPOSE 80:8000

# Working Directory
WORKDIR /home/ubuntu/uwsgi_cloud

# Copy contents of workdir to container
COPY . .


# Install packages
RUN apt-get update \
	&& apt-get install -y python3 python3.6-dev python3-pip npm memcached nginx libmemcached-dev zlib1g-dev\
	&& pip3 install -r lab4_cloudnet/docker_req.txt \
	&& npm install material-ui-icons@1.0.0-beta.17 \
	&& npm install material-ui@1.0.0-beta.34 \
#	&& ln -s lab4_cloudnet/mysite_nginx.conf /etc/nginx/sites-enabled/ \
#	&& ln -s lab4_cloudnet/mysite_nginx.conf /etc/nginx/sites-available/ \
	&& rm -rf /etc/nginx/sites-enabled \
	&& mkdir /etc/nginx/sites-enabled \
	&& ln -s ~/home/ubuntu/uwsgi_cloud/lab4_cloudnet/mysite_nginx.conf /etc/nginx/sites-enabled/

# start app

CMD /etc/init.d/nginx start \
	&& uwsgi --socket /lab4_cloudnet/mysite.sock --wsgi-file lab4_cloudnet/cloud_net/wsgi.py --chmod-socket=666
