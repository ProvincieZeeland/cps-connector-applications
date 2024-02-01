# Elasticsearch / Kibana
Elasticsearch is used to store content metadata (and in case of a PDF document, also the text representation for that PDF) and transaction data.

The install is based on the original Elasticsearch Docker install (https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html) but with following changes:

- For now we're running only one Elastic node, a feature TODO is create a high-availability cluster.
- Added our custom labels (used in Dashboard to group containers)
- Added volumes for data and snapshots
- Added security options
- Added restart options
- Added logging
- Added healthchecks

## Get started
Copy the ```env-example``` file to ```.env``` and setup the variables. The install is based on a setup container which creates certificates, in case you need to force creation of new certificates use the ```docker-compose-setup-force.yml``` file.

When the ```es-db``` and the ```es-kibana``` containers both are running use Kibana to setup indices etc, browse to http://localhost:5601/ and login with user elastic and the password specified in de ```.env``` file. Click the hamburger-menu (top-left) and browse all the way down to Management / Dev tools which starts a console.

- Open the ```indices-setup.txt``` file, copy the contents and paste it into the console in the Kibana window.


## Snapshots (backup)
Backup for Elasticsearch is done using snapshots, open ```snapshot-setup.txt``` and copy/paste the contents into the Kibana console.
It creates 2 snapshot repo's (ACC and PROD) and uses SLM (Snapshot Lifecycle Management) to automate the nightly updates. After executing the commands browse to Management / Stack management and click Snapshot and restore / Respositories. The screen should look like this:
![Schermafbeelding 2024-02-01 om 17 34 15](https://github.com/ProvincieZeeland/cps-connector-applications/assets/196572/fbaac1d6-8187-44e1-a170-53f241312ded)











