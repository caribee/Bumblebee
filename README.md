# Getting Started With Bumblebee

##### Pre-Requisites
You must have Go installed on your machine.

[![CircleCI](https://circleci.com/gh/caribeee/Bumblebee.svg?style=svg)](https://circleci.com/gh/caribeee/Bumblebee)

Dillinger is a cloud-enabled, mobile-ready, offline-storage, AngularJS powered HTML5 Markdown editor

### Installation

 * Clone the repository to the go src folder on your machine. To do that please run the following command :
    ``` git clone https://github.com/caribee/Bumblebee.git ```
 * Building the CLI. To build the CLI run the following commands:
    ```sh 
        cd <path_to_repo>/cli
        go build 
    ```
* To install the platform dependencies run the following commands:
     ``` sh
        go get -u github.com/golang/dep/cmd/dep
        go get -u github.com/jteeuwen/go-bindata/...
        go get -u github.com/pointlander/peg
        cd $GOPATH/src/github.com
        mkdir apex && cd apex
        git clone https://github.com/apex/up.git
        cd up
        git checkout f9e6f9ea84fad0902741d4beee4e36f67728cac4
        dep enusre
        cd internal && go generate ./...
    ```
*  Install ngrok and configure Hangouts Chat. Please follow the steps:
    * Download ngrok.
    * Login to your ngrok account and set the auth token by running the following command:
    ```sh 
            ./ngrok authtoken <your_auth_token>
    ```
    * To start ngrok run the following:
    ```sh
        cd <path_to_repo>
        ~/Downloads/ngrok start --config ngrok.yml --config ~/.ngrok2/ngrok.yml --all
    ```
    (considering the file downloaded is in the Downloads folder)
    * Copy the tunneling url and add it to the configuration of your Hangouts Chat API for your Google Cloud Project as the ``` Bot URL. ```
    * Give the email ids for the users who would have permissions to access the bot and click ``` Save. ```
* Installing overmind. To install overmind, run the following:
   ```sh
        brew install tmux
        brew install overmind    
    ```
    Add to Procfile what you want to run using overmind. To start overmind run ``` overmind start ``` or ``` overmind s ```
    If you have firewall enabled on your machine you may need to allow incoming connections.
* Create a new Google Cloud Project.
* Create a new Dialogflow agent and connect it to the Google Cloud Project you created.
*  Create new Google Application Credentials. Please follow the steps to generate the credentials.
    *  Open the Google Cloud Project you just created and click on ``` IAM and admin ```
    *  Go to ``` Service Accounts ```
    *  Click on ``` Create Service Account ```
    *  Set Permissions as ``` Dialogflow admin ```, ``` Service Account Token Creator ```
    *  Download the Key file.
    *  Base64 encode the key file contents.
    *  Create an Env variable named GOOGLE_APPLICATION_CREDENTIALS and set its value as the base64 encoded value you just created.
* Setting up the local Dynamo DB:
    * Download the zip from the [URL](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DynamoDBLocal.DownloadingAndRunning.html) & unzip it.  
    * Export all the required env vars. Run the following commands to export all the necessary env vars. 
    ```sh 
        export AWS_REGION=us-east-1
        export DYNAMO_ENDPOINT=http://localhost:8000
        export DYNAMO_DB_NAME=planet_dev
    ```
    * Create an entry for local dynamodb profile.
    ``` 
        vi ~/.aws/credentials
    ```
     Add the following to the file:
     ```
        [local_dynamodb]
        aws_access_key_id = <someKeyID>
        aws_secret_access_key = <someSecretAccessKey>
    ```
    To activate this profile ``` export AWS_PROFILE=local_dynamodb ``` in the terminal.
    * In a new terminal ``` export AWS_PROFILE=local_dynamodb ``` and run ``` java -Djava.library.path=./DynamoDBLocal_lib -jar DynamoDBLocal.jar ```
    * In another terminal set up the admin interface by running the following commands:
        * ```  npm install dynamodb-admin -g ```
        * Update the access and secret keys with same values as the ones in ``` ~/.aws/credentials ``` in the start_dynamodb_admin.sh file and start admin using ``` ./start_dynamodb_admin.sh ```
    * Access it at ``` http://0.0.0.0:8001/ ``` in your browser.

