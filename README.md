# Build the nginx from source

### Update and Install Dependencies for NGINX

```
apt-get update
```

- update command will update container and due to this command, other command will be executed smoothly

```
apt-get install build-essential libpcre3 libpcre3-dev zlib1g zlib1g-dev libssl-dev libgd-dev libxml2 libxml2-dev uuid-dev
```
- In this command we are installing all dependency 
- If you face timezone issue you can use `ln -snf /usr/share/zoneinfo/India /etc/localtime && echo India > /etc/timezone` this command and will set you timezone
- [depedency](https://github.com/ashjd1/docker-log-files/blob/master/dependency.log) log file

### Download NGINX Source Code and Configure

```
wget  http://nginx.org/download/nginx-1.20.0.tar.gz
```
- This command will download the nginx provided version
- Here wget used, the use of wget is, you can install dependency even if user is not logged in
- If this command won't work for your machine you can try `apt-get install wget` to install wget
- [wget](https://github.com/ashjd1/docker-log-files/blob/master/wget.log) log file

```
tar -zxvf nginx-1.20.0.tar.gz
```
- Use of tar command to create compressed or uncompressed archive files
- We have used here to extract nginx file
- [tar](https://github.com/ashjd1/docker-log-files/blob/master/tar.log) log file

```
cd nginx-1.20.0
```
- change directory

```
./configure --prefix=/var/www/html --sbin-path=/usr/sbin/nginx --conf-path=/etc/nginx/nginx.conf --http-log-path=/var/log/nginx/access.log --error-log-path=/var/log/nginx/error.log --with-pcre  --lock-path=/var/lock/nginx.lock --pid-path=/var/run/nginx.pid --with-http_ssl_module --with-http_image_filter_module=dynamic --modules-path=/etc/nginx/modules --with-http_v2_module --with-stream=dynamic --with-http_addition_module --with-http_mp4_module
```
- In the above command, we configured our custom path for the nginx configuration file, access, and Error Log path with nginx module
- [configure](https://github.com/ashjd1/docker-log-files/blob/master/config.log) log file

### Build NGINX & Adding Modules

```
./configure --without-http_empty_gif_module
```
- If you want to disable any module you can use `./configure --without-"module-name"`
- Here we are disable `http_empty_gif_module`
- [config-without](https://github.com/ashjd1/docker-log-files/blob/master/config-without.log) log file
### Compiling the NGINX source code

```
make 
```
- This make command will trigger all targets that are present in source code
- Basically this command will compile the source code
- [make](https://github.com/ashjd1/docker-log-files/blob/master/make.log) log file

```
make install
```
- installing nginx 
- If you mention any target, like here have mentioned `install` then this target will be executed only from source code
- [make-install](https://github.com/ashjd1/docker-log-files/blob/master/make-install.log) log file

```
nginx
```
- nginx command will start the nginx 
- If you get `bash: nginx: command not found` this error then you need to set you path
- you can do that using `export PATH=$PATH:/usr/local/nginx/sbin` this command 
- Then try `nginx` command again and niginx will get start

```
nginx -v
```
- This command will print the version of nginx 
- This command is for confirmation that we have installed
