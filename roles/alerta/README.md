# Alerta

This role will install alerta ( http://alerta.io/ ) along with the prometheus alerta plugin.

The alerta monitoring system is a tool used to consolidate and de-duplicate alerts from multiple sources for quick ‘at-a-glance’ visualization. Alerta can be used as a part of monitoring stack to provide a dashboards for all the alerts that get generated from monitoring. Alerta can be integrated with Prometheus-Alertmanager, alerts that are acknowledged in alerta get silenced in the alertmanager.

- Supported OS
  - Centos/Redhat 7


Example Playbook
----------------

    - hosts: alerta
      roles:
        - alerta
      tags:
        - alerta      
      become: true


`ansible-playbook alerta.yml -i /path/to/my/inventory`

## Dependencies
This role assumes that nginx and mongodb is already installed on the server


## Deploying and Running Alerta
After deploying alerta using the ansible role, the following changes have to be made -

Modify the alerta configuration ( /etc/alertad.conf ) to specify the alertmanager_api_url i.e. replace localhost with the ip/hostname of the actual server where you are running alertmanager.

    ALERTMANAGER_API_URL = 'http://localhost:9093'

Restart uwsgi service so that the modified configuration is picked up

    systemctl restart uwsgi

In the alerta UI create a new account, generate an Alerta API key with read and write permission to be used for integrating with alertmanager on the prometheus server for example -

vi /etc/prometheus/alertmanager.yml #replace api-key=withyouractualkey below

```
    receivers:
      - name: 'default-notifier'
        webhook_configs:
        - url: 'http://localhost:8080/api/webhooks/prometheus?api-key=GHPosk54asfkjkhfA51IOli'
          send_resolved: true
```
Reload the alertmanager configuration

    curl -X POST http://localhost:9093/-/reload

Check the alertmanager log file to see if there were any errors with the config - tail /var/log/prometheus/alertmanager.log (You may have the log file at a different location)

###Important Files

Alerta Configuration - /etc/alertad.conf
Alerta Log File - /var/log/alerta/alerta.log

###Troubleshooting

If the About page ( http://localhost:8080/#/about ) or the API page ( http://localhost:8080/api/ ) is not working properly you may want to check the status of uwsgi service


To enabled more verbose logging append the following in the alerta configuration file /etc/alertad.conf
 DEBUG = True
