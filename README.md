# Natural Language Classifier Demo Application

You can choose to run your app on Bluemix, or locally.

## Run your app on Bluemix

1. [Create and train an instance of the Watson Natural Language Classifier](https://watson.stage1.mybluemix.net/doc/nl-classifier/get_start.shtml).

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

1. Update the [app.js](app.js#L33) file with the classifier id in the response from the API when you create the classifier.

1. Push your app to make it live:

	```sh
	$ cf push
	```

1. Your service is now live and your app is hosted at `<application-name>.mybluemix.net`.



## Run your app locally

1. [Create and train an instance of the Watson Natural Language Classifier](https://watson.stage1.mybluemix.net/doc/nl-classifier/get_start.shtml).

1. Download and install [Node.js](http://nodejs.org/) and [npm](https://www.npmjs.com/).

1. Configure the code to connect to your service:

	1. Copy the credentials from your `natural-language-classifier-service` service. Run the following command:

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


## Troubleshooting

* See the [documentation][nlc_docs] for the Natural Language Classifier.

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
