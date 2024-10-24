# strato-certbot
Wildcard certificates for strato.de

##Install Cerbot in

Run `sudo apt update`
Run `sudo apt install certbot python3-certbot-nginx`

##Install python dependence

Run `pip install -r requirements.txt` 

## Setup

Change `strato-auth.json`:

```json
{
  "api_url": "https://www.strato.se/apps/CustomerService",
  "username": "<username>",
  "password": "<password>"
}
```

The api url needs to be filled with the correct url from your country. 
So as an example for Germany its 'https://www.strato.se/apps/CustomerService', but for the Netherlands its 'https://www.strato.nl/apps/CustomerService#skl'

Make sure to make this file only readable for root:

`sudo chmod 0400 strato-auth.json`

```

### Waiting time

Sometimes it takes a while until the desired DNS record is published, which allows Certbot to verify the domain. To prevent this, a waiting time can be set.

```json
{
  "api_url": "https://www.strato.se/apps/CustomerService",
  "username": "<username>",
  "password": "<password>",
  "waiting_time": <seconds>
}
```

## Get certificate

Run Certbot in manual mode:

`sudo certbot certonly --manual --preferred-challenges dns --manual-auth-hook $(pwd)/auth-hook.py --manual-cleanup-hook $(pwd)/cleanup-hook.py -d example.com -d *.example.com`

This will generate a wildcard certificate for your domain without the need to manually enter the TXT records.

