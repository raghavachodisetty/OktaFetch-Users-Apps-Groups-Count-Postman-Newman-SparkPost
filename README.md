# OktaFetch-Users-Apps-Groups-Count-Postman-Newman-SparkPost
This simple postman snippet will fetch users/apps/groups count from your okta instance. Additionally, SparkPost API script is configured as well in this Postman collection to trigger mail. However, make sure to get one SparkPost account before configuring email.

# okta-user-count-fetch-via-postman-newman

This code will fetch active/staged users count from Okta using postman. This code have the ability to filter out user count via custom attributes as well. This can run in Postman or Newman as well. If you are planning to run this code in an enterprise windows server, then newman alone should be enough to run this code.

***CONTENTS OF THIS REPOSITORY***

####  okta_users_count_with_custom_filters.postman_collection.json

You don't have to make any changes to this file unless you want to customize it with your own custom attribute filters.This json file is the key file and it has 3 API Request.

***1. Okta_InitializeEnvironment*** - This request will initialize the environment with all the required environment variables and API Call URL. Once done, it will call the next request (Fetch_Users_From_Okta).

***2. Okta_FetchUsers*** - This request will fetch users from Okta and will run continuously against your Okta environment until all the users are processed.

***3. Okta_FetchDeprovisionedUsers*** - This request will fetch deprovisioned users from Okta and will run continuously against your Okta environment until all the users are processed.

***4. Okta_FetchGroups*** - This request will fetch groups from Okta and will run continuously against your Okta environment until all the groups are processed.

***5. Okta_FetchApps*** - This request will fetch apps from Okta and will run continuously against your Okta environment until all the apps are processed.

***6. Trigger_Spark_Mail*** - This is an additional request to trigger email about the status of this run. To use this request, you need a SparkPost account with verified domain and API Token. Even without this request, all the results will be posted in the console.

***7. Okta_RestoreEnvironment*** - This request will restore your environment.


#### postman_environment.json

This file have the Okta instance details and API tokens as well. Replace values in below code and save this file.

```
{
	"id": "829f7893-48bd-4af7-ae8f-fba5fe294bf8",
	"name": "<replace this with environment name, example: OktaDev>",
	"values": [
		{
			"key": "url",
			"value": "<replace this with Okta instance URL>",
			"enabled": true
		},
		{
			"key": "apikey",
			"value": "<replace this with Okta API Token>",
			"enabled": true
		},
		{
			"key": "spark_api_key",
			"value": "<replace this with SparkPost API token",
			"enabled": true
		},
		{
			"key": "senderMail",
			"value": "<replace this with senders email>",
			"enabled": true
		},
		{
			"key": "recipentEmail",
			"value": "<replace this with recipents email id>",
			"enabled": true
		}
	],
	"_postman_variable_scope": "environment",
	"_postman_exported_at": "2020-05-06T10:15:42.389Z",
	"_postman_exported_using": "Postman/7.23.0"
}

```

***SETUP & REQUIREMENTS***

You either need postman or newman to run this code. Check below links to install postman and newman.

#### Setup Newman

If you have NPM installed, install Newman by running below command in your CMD.
```
npm install -g newman
```
If you dont have npm, check below link to setup node along with Newman.

> https://learning.postman.com/docs/postman/collection-runs/command-line-integration-with-newman/

#### Setup Postman

Below links will help you in configuring your Okta environment with Postman.

1. https://developer.okta.com/code/rest/
2. https://www.postman.com/downloads/


***RUNNING THIS CODE***

#### Running in Newman

Navigate to the directory where these files are located. Run below command. 
```
newman run OktaFetch-UsersAppsGroups-Count.postman_collection -e postman_environment.json
```

#### Running in Postman

Once postman is installed, import kta_users_count_with_custom_filters.postman_collection.json as a collection. Also import postman_environment.json as environment.

1. Open New Runner
2. Choose the Collection which you just imported
3. Choose Environment
4. Run

### NOTE
This code took around 16 minutes to pull out user count of 70000 in my Okta instance. It is taking around 3 seconds to 5 seconds to complete one API call.


#### If you are seeing any errors, do let me know. I will check and respond accordingly.
