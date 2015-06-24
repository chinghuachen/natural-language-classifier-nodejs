# Natural Language Classifier Nodejs Starter Application

Follow the instructions here to create a Classifier service instance on Bluemix. By default, the app will be hosted on Bluemix. If you prefer to host your app locally, additional instructions are provided.

## Create a classifier instance

1. You need a Bluemix account. If you don't have one, [sign up][sign_up]. Experimental Watson Services are free to use.

1. Download and install the [Cloud-foundry CLI][cloud_foundry] tool. This is required for communicating with the service on Bluemix.

1. Edit the `manifest.yml` file and change `<application-name>` to something unique. The name you use determines the URL of your application. For example, `<application-name>.mybluemix.net`.
	
	```
	applications:
	- services:
	  - natural-language-classifier-service
	  name: <application-name>
	  command: node app.js
	  path: .
	  memory: 128M
	```

1. Connect to Bluemix with the command line tool.
	
	```sh
	$ cf api https://api.ng.bluemix.net
	$ cf login -u <your user ID>
	```

1. Create the Natural Language Classifier service in Bluemix.
	
	```sh
	$ cf create-service natural_language_classifier free natural-language-classifier-service
	```

1. Update the [app.js](app.js#L33) file with the classifier id in the response from the API when you create the classifier.

1. Make your service live:

	```sh
	$ cf push
	```

1. Your service is now live and your app is hosted at `<application-name>.mybluemix.net`. However, to get the service to respond to input, you need to obtain service credentials and train the Classifier. For instructions on how to do this, refer to our general documentation [here](https://watson.stage1.mybluemix.net/doc/nl-classifier/get_start.shtml).



## Running locally

If you prefer to host your app locally, follow these steps after you have completed all of the above steps.

1. Download and install [Node.js](http://nodejs.org/) and [npm](https://www.npmjs.com/).

1. Configure the code to connect to your service:

	1. Copy the credentials from your `natural-language-classifier-service` service in Bluemix. Run the following command:

		```sh
		$ cf env <application-name>
		```

		Example output:

		```sh
		System-Provided:
		{
		  "VCAP_SERVICES": {
			"natural_language_classifier": [
			  {
				"credentials": {
				  "password": "<password>",
				  "url": "<url>",
				  "username": "<username>"
				}
				"label": "natural-language-classifier",
				"name": "natural-language-classifier-service",
				"plan": "free",
				"tags": [
				  ... 
				]
			  }
			]
		  }
		}
		```

	1. Copy `username`, `password`, and `url` from the credentials.
	1. Open the `app.js` file and paste the username, password, and url credentials for the service.
	1. Save the `creds.js` file.


1. Install the Natural Language Classifier Node.js package:
	1. Change to the new directory that contains the project. 
	2. Run the following command:node

	```node
	$ npm install
	```

1. Run the following command to start the application:

	```node
	node app.js
	```

1. Point your browser to [http://localhost:3000](http://localhost:3000).

1. Train the Classifier to get it to respond to your questions. For instructions on how to do this, refer to our general documentation [here](https://watson.stage1.mybluemix.net/doc/nl-classifier/get_start.shtml).


## Troubleshooting

* The main source of troubleshooting and recovery information is the Bluemix log. To view the log, run the following command:

  ```sh
  $ cf logs <application-name> --recent
  ```

* For more details about the service, see the [documentation][nlc_docs] for the Natural Language Classifier.

## License

  This sample code is licensed under Apache 2.0. Full license text is available in [LICENSE](LICENSE).  
  This sample uses [jquery](https://jquery.com/) which is MIT license
## Contributing

  See [CONTRIBUTING](CONTRIBUTING.md).

## Open Source @ IBM
  Find more open source projects on the [IBM Github Page](http://ibm.github.io/)

[cloud_foundry]: https://github.com/cloudfoundry/cli
[getting_started]: http://www.ibm.com/smarterplanet/us/en/ibmwatson/developercloud/doc/getting_started/
[nlc_docs]: http://www.ibm.com/smarterplanet/us/en/ibmwatson/developercloud/doc/nl-classifier/
[sign_up]: https://apps.admin.ibmcloud.com/manage/trial/bluemix.html?cm_mmc=WatsonDeveloperCloud-_-LandingSiteGetStarted-_-x-_-CreateAnAccountOnBluemixCLI
