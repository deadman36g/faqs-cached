<h1>Host a virtual host on your Feral slot</h1>

        
<br>
<h2>Virtual host aka vhost configuration</h2><br>
The steps will similar for any other domain name provider. The DNS settings and tools may differ from place to place but the basic idea is the same anywhere you go.<br>
<br>
<strong>STEP 1:</strong> Register Your Domain Name through a registrar.<br>
<br>
The best option to it register a top level domain such a <code>.com</code> or <code>.co.uk</code> (depending on your region). If the privacy of domain registration is an issue that is something you must consider before linking your domain to your Feral account. Once you are in control of a valid domain proceed with the guide.<br>
<br>
<strong>STEP 2:</strong> Obtain the IP of Your Feral Server to configure your DNS settings.<br>
<br>
You need this IP of your Feral slot in order to configure the DNS settings&#x2F;Records.<br>
<br>
You can get this information using SSH. <a href="https://www.feralhosting.com/faq/view?question=12">SSH to your server</a>, and type:<br>
<br>
<pre><code>hostname -i</code></pre><br>
or in IRC do, where <code>servername</code> is the name of your server:<br>
<br>
<pre><code>$ip servername</code></pre><br>
For example:<br>
<br>
<pre><code>$ip pontus</code></pre><br>
Take note of your server&#x27;s IP address, as you will need in the next step.<br>
<br>
<strong>STEP 3:</strong> Configure Your Domain Name using DNS settings:<br>
<br>
The DNS settings of any domain are controlled by the host of the Name Servers. If you have changed the name servers at some point you must use their DNS manager to configure the DNS records. By default you names servers should be controlled by the registrar post registration.<br>
<br>
<strong>Important note:</strong> Feral does not provide or manage name servers.<br>
<br>
Optionally, for this FAQ I recommend using this DNS service: <a href="http://rage4.com/">http:&#x2F;&#x2F;rage4.com&#x2F;</a> - See this page for namerserver settings - <a href="http://gbshouse.uservoice.com/knowledgebase/articles/107710-rage4-dns-frequently-asked-questions-faq-">Nameservers</a><br>
<br>
Your domain registrar or name server host will provide you with basic or advanced tools (a DNS records editor) to manage your DNS settings for each domain they are managing the name servers for. Find their DNS Settings Manager or similar and then we are going to two main records for this domain. The first is an <code>A</code> record for the main IP and the second will be a <code>cname</code> for the <code>www</code> version. Click on the domain name you&#x27;d like to configure, and then click the <code>Manage DNS</code> or similar options.<br>
<br>
We are going to create two new records for our custom domain. 1: an <code>A</code> record linking to the server IP and 2: a <code>CNAME</code> to redirect the <code>www</code> subdomain to the main A record<br>
<br>
<strong>Important note:</strong> Some hosting providers will automatically create a <code>CNAME</code> for your www version, such a GoDaddy. In this case you should only need to create Record 1, the <code>A</code> record. <br>
<br>
<strong>Record 1 A record:</strong> <code>example.co.uk</code> pointing to <code>123.123.123.123</code><br>
<br>
<strong>Record 2 CNAME record:</strong> <code>www.example.co.uk</code> pointing to <code>example.co.uk</code><br>
<br>
Here are the example records we use for the <code>example.co.uk</code> domain.<br>
<br>
<strong>Record 1 A record:</strong><br>
<br>
<img src="https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Host%20a%20virtual%20host%20on%20your%20Feral%20slot/1.png"><br>
<br>
<strong>Host</strong>: <code>example.co.uk</code><br>
<br>
<strong>TTL</strong>: <code>1H</code> or <code>3600</code><br>
<br>
<strong>Type</strong>: <code>A</code><br>
<br>
<strong>Value</strong>: The IP of your Feral server<br>
<br>
Add this new Record.<br>
<br>
<strong>Record 2 CNAME record:</strong><br>
<br>
<img src="https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Host%20a%20virtual%20host%20on%20your%20Feral%20slot/2.png"><br>
<br>
<strong>Host</strong>: <code>www.example.co.uk</code><br>
<br>
<strong>TTL</strong>: <code>1H</code> or <code>3600</code><br>
<br>
<strong>Type</strong>: <code>CNAME</code><br>
<br>
<strong>Value</strong>: <code>example.co.uk</code><br>
<br>
Add this new Record.<br>
<br>
<strong>Important Note:</strong> Activating domains can take up to 24 hours while the DNS propagates fully. This is beyond Feral&#x27;s control and you should consider changing your DNS servers if your ISP is taking too long to acknowledge the changes.<br>
<br>
<a href="https://developers.google.com/speed/public-dns/">Google DNS</a><br>
<br>
<a href="http://www.comodo.com/secure-dns/">Comodo DNS</a><br>
<br>
<a href="http://www.opendns.com/">OpenDNS</a><br>
<br>
<strong>STEP 4: Add it to the Server</strong><br>
<br>
After you&#x27;re done with the above steps, simply create a new folder with the same name as the domain inside the <code>~&#x2F;www</code> directory on your slot. All slots have this directory in their root location.<br>
<br>
<strong>Folder name:</strong> <code>example.co.uk</code><br>
<br>
So you will have something that looks like this:<br>
<br>
<img src="https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Host%20a%20virtual%20host%20on%20your%20Feral%20slot/3.png"><br>
<br>
It should be added almost immediately and when it is, another folder &quot;public_html&quot; should be created inside of each folder.<br>
<br>
The final directory structure will look something like:<br>
<br>
<pre><code>&#x2F;media&#x2F;12345&#x2F;home&#x2F;username&#x2F;www&#x2F;example.co.uk&#x2F;public_html&#x2F;</code></pre><br>
When you visit your domain&#x27;s URL in a browser you will be seeing any files that are inside the <code>public_html</code> directory.<br>
<br>
Now visit your website URL in a browser. You may need to clear your browser cache in some case to see the change.<br>
<br>
<br>
<h2>nginx</h2><br>
If you have followed this FAQ - <a href="https://www.feralhosting.com/faq/view?question=231">Updating Apache to nginx</a> then you will need to add your virtual hosts to nginx manually. Make sure you have pointed the DNS of your domain to the Feral server you want to host the domain on. Then follow this template:<br>
<br>
Change example.com to your domain name in these examples:<br>
<br>
<pre><code>mkdir -p ~&#x2F;www&#x2F;example.co.uk&#x2F;public_html
echo &#x27;www root&#x27; &gt; ~&#x2F;www&#x2F;example.co.uk&#x2F;public_html&#x2F;index.html</code></pre><br>
Show full path to the root:<br>
<br>
<pre><code>ls -d ~&#x2F;www&#x2F;example.co.uk&#x2F;public_html</code></pre><br>
Add this to a new file on the&nbsp; <code>~&#x2F;.nginx&#x2F;conf.d&#x2F;</code> directory. For example: <code>example.conf</code><br>
<br>
<strong>1:</strong> <code>example.co.uk</code> to your custom domain <br>
<strong>2:</strong> <code>root</code> to the result of the ls command above<br>
<strong>3:</strong> <code>fastcgi_pass</code> with your path info<br>
<br>
<pre><code>server {
&nbsp; &nbsp; listen&nbsp; &nbsp; &nbsp; 8080;
&nbsp; &nbsp; server_name example.co.uk *.example.co.uk;
&nbsp; &nbsp; root&nbsp; &nbsp; &nbsp; &nbsp; &#x2F;media&#x2F;DiskID&#x2F;home&#x2F;username&#x2F;www&#x2F;example.co.uk&#x2F;public_html;
&nbsp; &nbsp; index&nbsp; &nbsp; &nbsp;  index.html index.php;

&nbsp; &nbsp; autoindex&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; on;
&nbsp; &nbsp; autoindex_exact_size off;
&nbsp; &nbsp; autoindex_localtime&nbsp; on;

&nbsp; &nbsp; # Pass files that end in .php to PHP
&nbsp; &nbsp; location ~ \.php$ {
&nbsp; &nbsp; &nbsp; &nbsp; fastcgi_read_timeout 1h;
&nbsp; &nbsp; &nbsp; &nbsp; fastcgi_send_timeout 10m;

&nbsp; &nbsp; &nbsp; &nbsp; include&nbsp; &nbsp; &nbsp; &#x2F;etc&#x2F;nginx&#x2F;fastcgi.conf;
&nbsp; &nbsp; &nbsp; &nbsp; fastcgi_pass unix:&#x2F;media&#x2F;DiskID&#x2F;home&#x2F;username&#x2F;.nginx&#x2F;php&#x2F;socket;
&nbsp; &nbsp; }

&nbsp; &nbsp; # Deny access to anything starting with .ht
&nbsp; &nbsp; location ~ &#x2F;\.ht {
&nbsp; &nbsp; &nbsp; &nbsp; deny&nbsp; all;
&nbsp; &nbsp; }

&nbsp; &nbsp; # Wordpress in the www root
&nbsp; &nbsp; #
&nbsp; &nbsp; #location &#x2F; {
&nbsp; &nbsp; #&nbsp; &nbsp; &nbsp; &nbsp; try_files $uri $uri&#x2F; &#x2F;index.php?$args;
&nbsp; &nbsp; #}

&nbsp; &nbsp; # Wordpress in a subdirectory
&nbsp; &nbsp; #
&nbsp; &nbsp; #location &#x2F;wordpress {
&nbsp; &nbsp; #&nbsp; &nbsp; &nbsp; &nbsp; try_files $uri $uri&#x2F; &#x2F;wordpress&#x2F;index.php?$args;
&nbsp; &nbsp; #}
}</code></pre><br>
Reload your nginx:<br>
<br>
<pre><code>&#x2F;usr&#x2F;sbin&#x2F;nginx -s reload -c ~&#x2F;.nginx&#x2F;nginx.conf</code></pre><br>
You should now be able to visit your domain in the browser and see the changes.<br>
<br>
<h2>proxy_pass on a&nbsp; custom domain:</h2><br>
Here is an example of a proxypass on your custom domain using nginx in the top level of your www.<br>
<br>
<strong>Important note:</strong> Your app will be required to use the host <code>10.0.0.1</code> and not <code>localhost</code> or <code>127.0.0.1</code>.<br>
<br>
<pre><code>location &#x2F; {&nbsp; &nbsp; 
&nbsp; &nbsp; proxy_set_header X-Real-IP $remote_addr;
&nbsp; &nbsp; proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
&nbsp; &nbsp; proxy_set_header Host $http_host;
&nbsp; &nbsp; proxy_set_header X-NginX-Proxy true;
&nbsp; &nbsp; 
&nbsp; &nbsp; rewrite &#x2F;(.*) &#x2F;$1 break;
&nbsp; &nbsp; proxy_pass <a href="http://10.0.0.1:PORT/&#x3B;">http:&#x2F;&#x2F;10.0.0.1:PORT&#x2F;;</a>
&nbsp; &nbsp; proxy_redirect off;
}</code></pre><br>
<br>
