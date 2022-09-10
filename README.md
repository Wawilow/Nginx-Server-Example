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
<code>sudo nano /lib/systemd/system/$your_site.service</code>
<p>Copy this</p>
<pre>
[Unit]
Description=$your_site

[Service]
Type=simple
Restart=always
RestartSec=5s
ExecStart=$path

[Install]
WantedBy=multi-user.target
</pre>
<p>Start your server service</p>
<code>sudo service $your_site start</code>
<code>sudo service $your_site status</code>

<p>Nginx settings</p>
<code>cd /etc/nginx/sites-available</code>
<code>sudo nano $your_domain</code>
<pre>
server {
    server_name $your_domain www.$your_domain;

    location / {
        proxy_pass http://localhost:9990;
    }
}
</pre>
<code>sudo ln -s /etc/nginx/sites-available/$your_domain /etc/nginx/sites-enabled/$your_domain</code>
<code>sudo nginx -s reload</code>
<p>That's end, now you can test your app</p>