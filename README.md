<h1>Nginx Site Example</h1>
<h2>Install instruction</h2>
<p>Install go, git and nginx</p>
<code>sudo apt-get update && sudo apt-get upgrade</code>
<code>sudo apt-get install nginx snapd</code>
<code>sudo snap install go --classic</code>
<p>Make variable with your site name and domain name</p>
<code>your_site=your_domain_name</code>
<code>your_domain=$your_site.com</code>
<p>Clone this repository</p>
<code>cd</code>
<code>mkdir $your_site</code>
<code>cd $your_site</code>
<code>git clone https://gitlab.com/wawilow/nginx-server-example.git</code>
<p>Build go app</p>
<code>go build main.go</code>
<code>path=$(readlink -f main)</code>
<p>Make service</p>
<code>echo [Unit]
Description=goweb

[Service]
Type=simple
Restart=always
RestartSec=5s
ExecStart=/home/user/go/go-web/main

[Install]
WantedBy=multi-user.target
</code>
<code>sudo nano /lib/systemd/system/$your_site.service</code>
