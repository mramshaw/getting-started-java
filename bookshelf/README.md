# Bookshelf - Shows Authentication and CRUD
## Completed Application

## Requirements
* Java JDK 8

  ```
  java -version
  ```
  
* [Apache Maven](http://maven.apache.org) 3.3.9 or greater

  ```
  mvn -v
  ```
  
* Update or [Install the Cloud SDK](https://cloud.google.com/sdk/)

  ```
  gcloud components update
  ```
  
* Update or install `app-engine-java`:

    ```
    gcloud components update app-engine-java
    ```

  OR

    ```
    gcloud components install app-engine-java
    ```

  If update is attempted but `app-engine-java` is not actually installed, `gcloud` will prompt as follows:

    ```
    gcloud components update app-engine-java
    You have specified individual components to update.  If you are trying
     to install new components, use:
      $ gcloud components install app-engine-java
    
    Do you want to run install instead (y/N)?  y
    ```

* Verify the cloud components:

  ```
  gcloud components list
  ```
  
  Note that the Python Extensions (`app-engine-python`) have been updated as well.

## Before you begin
* Create a cloud Project using [Cloud Developer Console](https://console.google.com)
  * Enable Billing
* Initialize the SDK; Be sure to set the correct project ID
  * `gcloud init`
* Create a Bucket for Image Storage
  * `gsutil mb gs://<your-project-id>-images`
  * `gsutil defacl set public-read gs://<your-project-id>-images`
* Enable Required APIs
  * Cloud Console > API Manager > Overview > Google APIs
    * Google Cloud Datastore API
    * Google Cloud Pub/Sub API
    * Google Cloud Storage JSON API
    * Stackdriver Logging API
    * Google+ API
* Create Web Credentials (To be changed later)
  * Cloud Console > API Manager > Credentials > OAuth Client ID
  * Web Application (You may be asked to create an OAuth Consent screen, please do so)
  * Enable two authorized JavaScript origins
    * `https://PROJECTID.appspot.com`  so that you can deploy to the internet later
    * `http://localhost:8080` so that you can run locally
  * Enable two authorized redirect URL's
    * `https://PROJECTID.appspot.com/oauth2callback`
    * `http://localhost:8080/oauth2callback`
  * Be sure to get both the ClientID and ClientSecret.
* Edit [pom.xml](pom.xml) It should look something like:
    ```xml
    <properties>
      <bookshelf.storageType>datastore</bookshelf.storageType> <!-- datastore or cloudsql -->
      <bookshelf.bucket></bookshelf.bucket>                    <!-- bucket you created earlier -->

      <callback.host>PROJECTID.appspot.com</callback.host>     <!-- Typically projectname.appspot.com -->

      <bookshelf.clientID></bookshelf.clientID>                <!-- for User Authentication -->
      <bookshelf.clientSecret></bookshelf.clientSecret>        <!-- from g.co/cloud/console -->
    </properties>
    ```

## Running locally

* In one of the subdirectories to this `README.md` file:

    mvn -Plocal clean jetty:run-exploded

* Visit `http://localhost:8080`

## Deploy to AppEngine Managed VMs

* In one of the subdirectories to this `README.md` file:

    mvn clean gcloud:deploy

* Visit `http://PROJECTID.appspot.com`.

## TODO

- [x] Verify with latest Cloud SDK (used `173.0.0`)
- [x] Verify with latest Java Extensions (used `1.9.56`)
- [x] Verify with latest Maven (used `3.5.0`)
- [ ] Verify with latest Java (used `openjdk version "1.8.0_131"`)
