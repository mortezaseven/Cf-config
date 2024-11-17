در این روش شما میتوانید با استفاده از آی پی کثیف سرور که پشت یک دامنه کثیف است ، از V2ray استفاده کنید
<br>
فقط به یک آی پی سالم کلودفلر نیاز دارید
<br>
پروکسی دامنه شما باید روشن باشد
<br>
روی چهار نت متفاوت تست شده
<br>
ابتدا یکی از پنل های XUI رو نصب کنید
<br>
اگر این روش کار نکرد ، به روشی که در ادامه گفته شده ، پنل رو نصب کنید
<br>
یک کانفیگ با مشخصات زیر بسازی
<br>
vless
<br>
transmission : SplitHTTP
<br>
Host : dirty domain ( with proxy on )
<br>
Path : /test?ed=2096
<br>
بجای کلمه test هر کلمه ای که مایل بودید را میتوانید بنویسید
<br>
external proxy = on
<br>
Ip : one of the clean cloudflare Ip
<br>
port : one of the cloudflare https ports
<br>
security : TLS
<br>
uTLS : chrome
<br>
ALPN : h2 - http/1.1 - h3
<br>
allow insecure : on
<br>
public and private key of dirty domain must insert
<br>
بقیه موارد را دست نزنید
<br>
<br>
<br>
<br>
<br>
<br>
<br>
---

پس از کپی کردن کانفیگ در سمت کاربر ، در کانفیک باید یک تغییر ایجاد کنید
ALPN : h3
دو مورد h2 , Http/1.1 حذف شود

---
روشی که من پنل رو نصب کردم و سرتیفیکت گرفتم از طریق Nginx هست
#update server
```
apt update && apt upgrade -y
```
#install nginx & Certbot
```
sudo apt install nginx certbot python3-certbot-nginx -y
```
#copy default NGINX to web
```
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/my.domain.ir
```
#enable website 
```
ln -s /etc/nginx/sites-available/my.domain.ir /etc/nginx/sites-enabled/
```
#test
```
cd /etc/nginx/sites-enabled && ls -la
```
#edit website config
```
nano /etc/nginx/sites-available/my.domain.ir
```
remove default values  
server_name my.domain.ir;
#restart NGINX service
```
systemctl restart nginx
```
#get ssl
```
certbot --nginx -d my.domain.ir --register-unsafely-without-email
```
#install xui
```
bash <(curl -Ls https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh)
```
#ssl direction

/etc/letsencrypt/live/my.domain.ir/fullchain.pem

/etc/letsencrypt/live/my.domain.ir/privkey.pem
