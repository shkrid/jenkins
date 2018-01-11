```
Started by GitHub push by shkrid
Obtained Jenkinsfile from git https://github.com/shkrid/jenkins.git
[Pipeline] node
Running on master in /var/jenkins_home/workspace/lua
[Pipeline] {
[Pipeline] stage
[Pipeline] { (Declarative: Checkout SCM)
[Pipeline] checkout
 > git rev-parse --is-inside-work-tree # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/shkrid/jenkins.git # timeout=10
Fetching upstream changes from https://github.com/shkrid/jenkins.git
 > git --version # timeout=10
 > git fetch --tags --progress https://github.com/shkrid/jenkins.git +refs/heads/*:refs/remotes/origin/*
 > git rev-parse refs/remotes/origin/master^{commit} # timeout=10
 > git rev-parse refs/remotes/origin/origin/master^{commit} # timeout=10
Checking out Revision f4ce4c2798c79ff3464f225b09aa7eb2407fc7d8 (refs/remotes/origin/master)
Commit message: "dummy"
 > git config core.sparsecheckout # timeout=10
 > git checkout -f f4ce4c2798c79ff3464f225b09aa7eb2407fc7d8
 > git rev-list d927cc488264878703d4ea911e9592383bdc2812 # timeout=10
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Build)
[Pipeline] echo
Building..
[Pipeline] sh
[lua] Running shell script
+ docker build -t shkrid/nginx-alpine:base-lua .
Sending build context to Docker daemon 13.31 kB

Step 1/10 : FROM alpine:3.4
 ---> c7fc7faf8c28
Step 2/10 : ENV LANG en_US.UTF-8
 ---> Using cache
 ---> 9e3ebcfc5d4f
Step 3/10 : RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories
 ---> Using cache
 ---> a43e34862c25
Step 4/10 : ENV NGINX_VERSION 1.10.2
 ---> Using cache
 ---> 2788c9fac672
Step 5/10 : ENV NGX_DEVEL_KIT_VERSION 0.3.0
 ---> Using cache
 ---> 2e5dca66b49b
Step 6/10 : ENV LUA_NGINX_MODULE_VERSION 0.10.7
 ---> Using cache
 ---> 370a12733bfd
Step 7/10 : RUN apk add --no-cache luajit
 ---> Using cache
 ---> 861fd0b12ed1
Step 8/10 : RUN GPG_KEYS=B0F4253373F8F6F510D42178520A9993A1C052F8 	&& CONFIG="		--prefix=/etc/nginx 		--sbin-path=/usr/sbin/nginx 		--modules-path=/usr/lib/nginx/modules 		--conf-path=/etc/nginx/nginx.conf 		--error-log-path=/var/log/nginx/error.log 		--http-log-path=/var/log/nginx/access.log 		--pid-path=/var/run/nginx.pid 		--lock-path=/var/run/nginx.lock 		--http-client-body-temp-path=/var/cache/nginx/client_temp 		--http-proxy-temp-path=/var/cache/nginx/proxy_temp 		--http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp 		--http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp 		--http-scgi-temp-path=/var/cache/nginx/scgi_temp 		--user=nginx 		--group=nginx 		--with-http_ssl_module 		--with-http_realip_module 		--with-http_addition_module 		--with-http_sub_module 		--with-http_dav_module 		--with-http_flv_module 		--with-http_mp4_module 		--with-http_gunzip_module 		--with-http_gzip_static_module 		--with-http_random_index_module 		--with-http_secure_link_module 		--with-http_stub_status_module 		--with-http_auth_request_module 		--with-http_xslt_module=dynamic 		--with-http_image_filter_module=dynamic 		--with-http_geoip_module=dynamic 		--with-http_perl_module=dynamic 		--with-threads 		--with-stream 		--with-stream_ssl_module 		--with-http_slice_module 		--with-mail 		--with-mail_ssl_module 		--with-file-aio 		--with-http_v2_module 		--with-ipv6 		--with-ld-opt="-Wl,-rpath,/usr/lib" 	  --add-module=/tmp/ngx_devel_kit-${NGX_DEVEL_KIT_VERSION} 	  --add-module=/tmp/lua-nginx-module-${LUA_NGINX_MODULE_VERSION} 	" 	&& addgroup -S nginx 	&& adduser -D -S -h /var/cache/nginx -s /sbin/nologin -G nginx nginx 	&& apk add --no-cache --virtual .build-deps 		gcc 		libc-dev 		make 		openssl-dev 		pcre-dev 		zlib-dev 		linux-headers 		curl 		gnupg 		libxslt-dev 		gd-dev 		geoip-dev 		perl-dev 		luajit-dev 	&& export LUAJIT_LIB=/usr/lib 	&& export LUAJIT_INC=/usr/include/luajit-2.0 	&& curl -fSL https://github.com/simpl/ngx_devel_kit/archive/v0.3.0.tar.gz -o /tmp/ndk.tar.gz 	&& tar -xvf /tmp/ndk.tar.gz -C /tmp 	&& curl -fSL https://github.com/openresty/lua-nginx-module/archive/v${LUA_NGINX_MODULE_VERSION}.tar.gz -o /tmp/lua-nginx.tar.gz 	&& tar -xvf /tmp/lua-nginx.tar.gz -C /tmp 	&& curl -fSL http://nginx.org/download/nginx-$NGINX_VERSION.tar.gz -o nginx.tar.gz 	&& curl -fSL http://nginx.org/download/nginx-$NGINX_VERSION.tar.gz.asc  -o nginx.tar.gz.asc 	&& export GNUPGHOME="$(mktemp -d)" 	&& gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$GPG_KEYS" 	&& gpg --batch --verify nginx.tar.gz.asc nginx.tar.gz 	&& rm -r "$GNUPGHOME" nginx.tar.gz.asc 	&& mkdir -p /usr/src 	&& tar -zxC /usr/src -f nginx.tar.gz 	&& rm nginx.tar.gz 	&& cd /usr/src/nginx-$NGINX_VERSION 	&& ./configure $CONFIG --with-debug 	&& make -j$(getconf _NPROCESSORS_ONLN) 	&& mv objs/nginx objs/nginx-debug 	&& mv objs/ngx_http_xslt_filter_module.so objs/ngx_http_xslt_filter_module-debug.so 	&& mv objs/ngx_http_image_filter_module.so objs/ngx_http_image_filter_module-debug.so 	&& mv objs/ngx_http_geoip_module.so objs/ngx_http_geoip_module-debug.so 	&& mv objs/ngx_http_perl_module.so objs/ngx_http_perl_module-debug.so 	&& ./configure $CONFIG 	&& make -j$(getconf _NPROCESSORS_ONLN) 	&& make install 	&& rm -rf /etc/nginx/html/ 	&& mkdir /etc/nginx/conf.d/ 	&& mkdir -p /usr/share/nginx/html/ 	&& install -m644 html/index.html /usr/share/nginx/html/ 	&& install -m644 html/50x.html /usr/share/nginx/html/ 	&& install -m755 objs/nginx-debug /usr/sbin/nginx-debug 	&& install -m755 objs/ngx_http_xslt_filter_module-debug.so /usr/lib/nginx/modules/ngx_http_xslt_filter_module-debug.so 	&& install -m755 objs/ngx_http_image_filter_module-debug.so /usr/lib/nginx/modules/ngx_http_image_filter_module-debug.so 	&& install -m755 objs/ngx_http_geoip_module-debug.so /usr/lib/nginx/modules/ngx_http_geoip_module-debug.so 	&& install -m755 objs/ngx_http_perl_module-debug.so /usr/lib/nginx/modules/ngx_http_perl_module-debug.so 	&& ln -s ../../usr/lib/nginx/modules /etc/nginx/modules 	&& strip /usr/sbin/nginx* 	&& strip /usr/lib/nginx/modules/*.so 	&& rm -rf /usr/src/nginx-$NGINX_VERSION 	&& rm -f /tmp/ndk.tar.gz 	&& rm -f /tmp/lua-nginx.tar.gz 	&& rm -rf /tmp/ngx_devel_kit-${NGX_DEVEL_KIT_VERSION} 	&& rm -rf /tmp/lua-nginx-module-${LUA_NGINX_MODULE_VERSION} 		&& apk add --no-cache --virtual .gettext gettext 	&& mv /usr/bin/envsubst /tmp/ 		&& runDeps="$( 		scanelf --needed --nobanner /usr/sbin/nginx /usr/lib/nginx/modules/*.so /tmp/envsubst 			| awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' 			| sort -u 			| xargs -r apk info --installed 			| sort -u 	)" 	&& apk add --no-cache --virtual .nginx-rundeps $runDeps 	&& apk del .build-deps 	&& apk del .gettext 	&& mv /tmp/envsubst /usr/local/bin/ 		&& ln -sf /dev/stdout /var/log/nginx/access.log 	&& ln -sf /dev/stderr /var/log/nginx/error.log
 ---> Using cache
 ---> 4bc5df76241d
Step 9/10 : EXPOSE 80 443
 ---> Using cache
 ---> 7c670ac3db19
Step 10/10 : CMD ["nginx", "-g", "daemon off;"]
 ---> Using cache
 ---> 18f25ad05d5c
Successfully built 18f25ad05d5c
Successfully tagged shkrid/nginx-alpine:base-lua
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Dockerize)
[Pipeline] echo
Dockerize..
[Pipeline] sh
[lua] Running shell script
+ docker build -t shkrid/nginx-alpine:custom -f Dockerfile-custom .
Sending build context to Docker daemon  7.68 kB

Step 1/4 : FROM shkrid/nginx-alpine:base-lua
 ---> 18f25ad05d5c
Step 2/4 : COPY nginx-custom.conf /etc/nginx/nginx.conf
 ---> Using cache
 ---> fed92a97e2cd
Step 3/4 : COPY nginx.vh.default.conf /etc/nginx/conf.d/default.conf
 ---> Using cache
 ---> c4ecf4a33013
Step 4/4 : COPY index.html /usr/share/nginx/html/index.html
 ---> Using cache
 ---> 91b1fe33e8b1
Successfully built 91b1fe33e8b1
Successfully tagged shkrid/nginx-alpine:custom
[Pipeline] withCredentials
[Pipeline] {
[Pipeline] sh
[lua] Running shell script
+ docker login -u **** -p ****
Login Succeeded
[Pipeline] sh
[lua] Running shell script
+ docker push ****/nginx-alpine:custom
The push refers to a repository [docker.io/****/nginx-alpine]
574c85697832: Preparing
0cd1ae3815b3: Preparing
03016ddd9024: Preparing
e9ac468744b0: Preparing
665c878b55c6: Preparing
14efe84c92a6: Preparing
e53f74215d12: Preparing
14efe84c92a6: Waiting
e53f74215d12: Waiting
574c85697832: Layer already exists
e9ac468744b0: Layer already exists
0cd1ae3815b3: Layer already exists
665c878b55c6: Layer already exists
03016ddd9024: Layer already exists
e53f74215d12: Layer already exists
14efe84c92a6: Layer already exists
custom: digest: sha256:0680f54c237e1aa765316a0ba11fd67b2c1a15cb6067477905671202e28fdd55 size: 1778
[Pipeline] }
[Pipeline] // withCredentials
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Deploy)
[Pipeline] echo
Deploying....commented out
[Pipeline] echo
docker-machine create --driver amazonec2 --amazonec2-access-key AKI******* --amazonec2-secret-key 8T93C******* aws-sandbox
[Pipeline] echo
eval "$(docker-machine env aws-sandbox)"; docker run -d -p 80:80 shkrid/nginx-alpine:custom
[Pipeline] echo
Check nginx modules
[Pipeline] sh
[lua] Running shell script
+ docker run --rm shkrid/nginx-alpine:custom nginx -V
nginx version: nginx/1.10.2
built by gcc 5.3.0 (Alpine 5.3.0) 
built with OpenSSL 1.0.2n  7 Dec 2017
TLS SNI support enabled
configure arguments: --prefix=/etc/nginx --sbin-path=/usr/sbin/nginx --modules-path=/usr/lib/nginx/modules --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --pid-path=/var/run/nginx.pid --lock-path=/var/run/nginx.lock --http-client-body-temp-path=/var/cache/nginx/client_temp --http-proxy-temp-path=/var/cache/nginx/proxy_temp --http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp --http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp --http-scgi-temp-path=/var/cache/nginx/scgi_temp --user=nginx --group=nginx --with-http_ssl_module --with-http_realip_module --with-http_addition_module --with-http_sub_module --with-http_dav_module --with-http_flv_module --with-http_mp4_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_random_index_module --with-http_secure_link_module --with-http_stub_status_module --with-http_auth_request_module --with-http_xslt_module=dynamic --with-http_image_filter_module=dynamic --with-http_geoip_module=dynamic --with-http_perl_module=dynamic --with-threads --with-stream --with-stream_ssl_module --with-http_slice_module --with-mail --with-mail_ssl_module --with-file-aio --with-http_v2_module --with-ipv6 --with-ld-opt=-Wl,-rpath,/usr/lib --add-module=/tmp/ngx_devel_kit-0.3.0 --add-module=/tmp/lua-nginx-module-0.10.7
[Pipeline] }
[Pipeline] // stage
[Pipeline] }
[Pipeline] // node
[Pipeline] End of Pipeline
Finished: SUCCESS
```
