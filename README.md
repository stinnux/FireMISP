python script for interacting with misp to push information from a FireEye Alert JSON to a MISP instance

Inspired by: https://github.com/spcampbell/FireStic

Runnning one or multiple FireEye systems there is a feature to send alerts to a given webserver.
The firemisp.py sets up a webserver to be able to receive the Alerts.
It will then process the alerts and use certain aspects of the alert and map it to MISP event.

pyFireEyeAlert is a mapper of FireEye Alert in a python class. New key - values pairs can be easily added to the mapping.


Installation
============

update the values to your needs

modify the API Key:
```
cp config.example.cfg config.cfg
vi config.cfg
#change the values
```

Running
=======

run the script (in that example 192.168.178 is the IP of MISP):

```
python firemisp/firemisp.py
INFO:requests.packages.urllib3.connectionpool:Starting new HTTP connection (1): 192.168.178.71
DEBUG:requests.packages.urllib3.connectionpool:"GET /servers/getVersion HTTP/1.1" 200 20
INFO:requests.packages.urllib3.connectionpool:Starting new HTTP connection (1): 10.50.12.71
DEBUG:requests.packages.urllib3.connectionpool:"GET /attributes/describeTypes.json HTTP/1.1" 200 4819
INFO:__main__:Starting HTTP server 127.0.0.1 8080

```


Testing
=======

To test with real data put your *.json files in testing/real (they will be ignored by git)

```
    python testing/fmtest.py -d testing/real
```

To test with sample data:#

```
    python testing/fmtest.py -f testing/alert_details_fireeye_reducted.json
```

If you do not have a MISP instance, you can get a VM with MISP at https://www.circl.lu/services/misp-training-materials/
Once you have that MISP instance running and reachable from the system you are running FireMisp, get the API key at

```
$YOURIPOFMISP/users/view/me
```

And edit the config.cfg according to your needs.

To delete events that have been created for test purposes, uncomment the section in firemisp.py

```
   #clean the database for test purposes
    '''for i in range (200,1348,1):
        misp.delete_event(i)
    exit()
   '''
```

And adjust the id values to your need


Issues
======

There is no
```
DEBUG:requests.packages.urllib3.connectionpool:"GET /servers/getVersion HTTP/1.1" 200 20
INFO:requests.packages.urllib3.connectionpool:Starting new HTTP connection (1): 10.50.12.71
```
After starting FireMisp.py

Instead:
```
pymisp.api.PyMISPError: Unable to connect to MISP (http://192.168.178.71). Please make sure the API key and the URL are correct (http/https is required): HTTPConnectionPool(host='192.168.178.71', port=80): Max retries exceeded with url: /servers/getVersion (Caused by <class 'socket.error'>: [Errno 110] Connection timed out)
```

That means the connection to the MISP instance.

Example:
========

To be done

Roadmap
=======

There are obviosly some things to be done in the future:
- improve current mappings (pyFireEyeAlert.py)
- make the mapping more robust (pyFireEyeAlert.py)
- introduce new mappings (FireMisp.py + pyFireEyeAlert.py)
- improve correlation (Feedback welcome)
- test it with high volume of alerts

# MISP
Want to learn about MISP: http://www.misp-project.org/

# MISP API
To learn about the MISP API, check out: https://github.com/MISP/PyMISP

# Idea
The idea is already mentioned in MISP featuhb: http://feathub.com/MISP/MISP/+3

# Next steps
- The pyFireEyeAlert class might be seperated to be re-usable once it reached a stable status
