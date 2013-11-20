NZBLandingPage
==============

I made this to remote access my home server, SABnzbd, SickBeard and CouchPotato.
The goal was to provide a nice UI for me and anyone else that uses it.


Required
==============
- Apache 2 (to host the website)
- SABnzbd, SickBeard, CouchPotato
- Basic text editor


Installation
==============
1. Install all the programs. Apache 2 can be downloaded from their website. Configure them as necessary (making sure you add the server and domain names for Apache during installation).

2. Open the Apache httpd.conf Configuration File. A shortcut can be found in the start-menu.

3. Uncomment the following by removing the '#' at the start of the line:

			LoadModule proxy_connect_module modules/mod_proxy_connect.so
			LoadModule proxy_http_module modules/mod_proxy_http.so
			LoadModule proxy_ftp_module modules/mod_proxy_ftp.so
			LoadModule negotiation_module modules/mod_negotiation.so
			LoadModule rewrite_module modules/mod_rewrite.so

4. Add the following to the end of the file, change the ports based on your installation:

			<Location /sabnzbd>
				order deny,allow
				deny from all
				allow from all
				ProxyPass http://localhost:8085/sabnzbd
				ProxyPassReverse http://localhost:8085/sabnzbd
			</Location>
			
			<Location /sickbeard/>
				order deny,allow
				deny from all
				allow from all
				ProxyPass http://localhost:8081/sickbeard/
				ProxyPassReverse http://localhost:8081/sickbeard/
			</Location>
			
			<Location /couchpotato/>
			    ProxyPass http://localhost:5050/couchpotato/
			    ProxyPassReverse http://localhost:5050/couchpotato/
			</Location>

5. Go to the Apache 2 installation folder and delete everything in the 'htdocs' folder

6. Copy and Paste my files in there

7. Shutdown SickBeard if running and open its 'config.ini' file in its installation directory. Make the value of 'web_root' to '/sickbeard'

8. Open CouchPotato, in Settings > General (advanced settings) change Url base to 'couchpotato'

8. Restart Apache 2

9. Open your browser and go to your domain

9. Finish
