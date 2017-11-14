# wordpress-security-htaccess
By default, every website hosting has .htaccess file in the root directory.


PROTECT .HTACCESS

.htaccess has the ability to control your whole website. It is important to first protect the .htaccess file from unauthorised users.

By using the snippet below, you can restrict access to unauthorised users.

You can edit the file from FTP and your cPanel hosting.

Just copy and paste the snippet below into your .htaccess file.

 <files ~ "^.*.([Hh][Tt][Aa])"> order allow,deny deny from all satisfy all </files> 
 
 
 
 
PROTECT WP-CONTENTS

Wp-contents is the folder in your WordPress directory that contains files of your themes, plugins, media and cached files.

That’s why this directory is the main target for hackers and spammers.

Create a separate .htaccess file.

Copy and paste the snippet below, in that file.

Order deny,allow Deny from all <Files ~ ".(xml|css|jpe?g|png|gif|js)$"> Allow from all </Files> 
 
 
Now, upload it to “yoursite.com/wp-contents/” folder.

By uploading this file, only media files are allowed to be uploaded including XML, CSS, JPG, JPEG, PNG, Gif, and Javascript. All other file types will be denied.



DISABLE DIRECTORY BROWSING

Many WordPress security experts recommend disabling directory browsing.

With directory browsing enabled, hackers can look into your site’s directory and file structure to find a vulnerable file.

To disable directory browsing on your website, you need to add the following line to your .htaccess file.

 Options -Indexes 
 
 
DISABLE IMAGE HOTLINKING

Other websites directly hot-linking images from your site can make your WordPress site slow and exceed your bandwidth limit.

This isn’t a big issue for most smaller websites. However, if you run a popular website or a website with lots of photos, then this could become a serious concern.

You can prevent image hot-linking by adding this code to your .htaccess file:

 #disable hot-linking of images with forbidden or custom image option RewriteEngine on RewriteCond %{HTTP_REFERER} !^$ RewriteCond %{HTTP_REFERER} !^http(s)?://(www.)?sitemaster.com.au [NC] RewriteCond %{HTTP_REFERER} !^http(s)?://(www.)?google.com [NC] RewriteRule .(jpg|jpeg|png|gif)$ – [NC,F,L] 
 
 
DISABLE ACCESS TO XML-RPC FILE

Each WordPress install comes with a file called xmlrpc.php. This file allows third-party apps to connect to your WordPress site.

Most WordPress security experts advise that if you are not using any third party apps, then you should disable this feature.

There are multiple ways to do that, one of them is by adding the following code to your .htaccess file:

 # Block WordPress xmlrpc.php requests <Files xmlrpc.php> order deny,allow deny from all </Files> 
 
 
PROTECT INCLUDE-ONLY FILES

There are some areas in WordPress that never have to be accessed by the user.

It’s better to block access to those files.

You can place blocks by adding the snippet below, into your .htaccess file.

 <IfModule mod_rewrite.c> RewriteEngine On RewriteBase / RewriteRule ^wp-admin/includes/ - [F,L] RewriteRule !^wp-includes/ - [S=3] RewriteRule ^wp-includes/[^/]+.php$ - [F,L] RewriteRule ^wp-includes/js/tinymce/langs/.+.php - [F,L] RewriteRule ^wp-includes/theme-compat/ - [F,L] </IfModule> 
 
 
REDIRECT A URL

A 301 error tells search engines that a URL has been permanently moved to another new location.

You can redirect that old URL to the new one by using .htaccess.

This is not limited to URLs only, you can redirect a folder, page or even a complete website.

You just have to add the few lines of code below, to your .htaccess file.

 Redirect 301 /oldpage.html https://yoursite.com Redirect 301 /oldfolder/page.html /folder6/page.html Redirect 301 / https://mynewsite.com/ 
 
 
PROTECT WP-CONFIG.PHP

In WordPress, wp-config.php is the file where your hosting, database and other important credentials are saved.

Therefore it is also required to restrict unauthorised access to this file.

Copy and paste lines of code  below, in your .htaccess file.

 <files wp-config.php> order allow,deny deny from all </files> 
 
 
BLOCKING AUTHOR SCANS

A common technique used in brute force attacks is to run author scans on a WordPress site and then attempt to crack passwords for those usernames.

You can block such scans by adding the following code to your .htaccess file:

 # BEGIN block author scans RewriteEngine On RewriteBase / RewriteCond %{QUERY_STRING} (author=d+) [NC] RewriteRule .* - [F] # END block author scans 
BAN IP ADDRESSES
Are you seeing unusually high requests to your website from a specific IP address?

You can easily block those requests by blocking the IP address in your .htaccess file

 <Limit GET POST> order allow,deny deny from 123.456.78.9 allow from all </Limit> 
PASSWORD PROTECT WORDPRESS ADMIN FOLDER
If you access your WordPress site from multiple locations including public internet spots, then limiting access to specific IP addresses may not work for you.

You can use .htaccess file to add an additional password protection to your WordPress admin area.

First, you need to generate a .htpasswds file.

You can easily create one by using this online generator.

Upload this .htpasswds file outside your publicly accessible web directory or /public_html/ folder. A good path would be:

/home/user/.htpasswds/public_html/wp-admin/passwd/

Next, create a .htaccess file and upload it in /wp-admin/ directory and then add the following codes in there:

 AuthName "Admins Only" AuthUserFile /home/yourdirectory/.htpasswds/public_html/wp-admin/passwd AuthGroupFile /dev/null AuthType basic require user putyourusernamehere <Files admin-ajax.php> Order allow,deny Allow from all Satisfy any </Files> 
Important: Don’t forget to replace AuthUserFile path with the file path of your .htpasswds file and add your own username.

DISABLE PHP EXECUTION IN SOME WORDPRESS DIRECTORIES
In WordPress, wp-config.php is the file where your hosting, database and other important credentials are saved.

Therefore it is also required to restrict unauthorised access to this file.

Copy and paste lines of code  below, in your .htaccess file.

 <files wp-config.php> order allow,deny deny from all </files> 
