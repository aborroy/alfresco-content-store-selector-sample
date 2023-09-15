# Sample Deployment for Alfresco Enteprise with Content Store Selector

[Content Store Selector](https://docs.alfresco.com/content-services/latest/admin/content-stores/#cs-selector) is only available for ACS Enterprise version. This feature allows to create additional Content Stores, so part of the repository can be stored on a different location.


## Docker Compose

This project includes sample configuration to use Alfresco Enteprise 7.4 add a sample Content Store `siteContentStore` (stored on the physical folder `${dir.root}/site`).


```
.
├── config
│   ├── content-store-selector-context.xml
│   └── share-config-custom-dev.xml
├── .env
└── docker-compose.yml
```

* `.env` includes Docker Image tag names
* `docker-compose.yml` is a regular ACS Docker Compose, mapping required configuration for `alfresco` and `share` services
* `config/content-store-selector-context.xml` includes a sample configuration to create a new Content Store named `siteStore`
* `config/share-config-custom-dev.xml` includes configuration to display the `cm:storeSelector` in Share UI

## Using

```
$ docker-compose up --build --force-recreate
```

## Configuration

Before uploading files to a new Site or Folder, apply following rule to targeted folder:

* Run in background
* Rule applied to subfolders
* When:
  * Items are created or enter this folder
* If all criteria are met:
  * All Items
* Perform Action:
  * Add 'ContentStore Selector' aspect
  * Set property valueProperty:Store NameValue:siteStore

Once the rule is applied, the files uploaded to this folder hierarchy will be stored on a new physical folder named `site`

```
$ pwd
/usr/local/tomcat/alf_data

$ ls -la
total 24
drwxr-x--- 3 alfresco alfresco 4096 Sep 15 14:13 contentstore
drwxr-x--- 2 alfresco alfresco 4096 Sep 15 14:13 contentstore.deleted
drwxr-x--- 2 alfresco alfresco 4096 Sep 15 14:13 site
```

## Service URLs

http://localhost:8080/share

Share

* user: admin
* password: admin

http://localhost:8080/alfresco

Alfresco Repository

* user: admin
* password: admin