# chrome-federated-learning-classifier
Implementation of federated learning js inside a Chrome Extension to classify web-page content


### App/
This folder contains an unpacked built version of the Disinformation Defender Chrome extension. It includes both the Presentation Layer and the client-side Application Logic 
within its bundled JS files. All you need to do to use it is:
1) Verify with me that the GCP instance is running so you can test
2) Clone or download the contents of the App/ directory and place them in a folder somewhere on your PC
3) Go into Chrome and set it to developer mode. Just go to Chrome://Extensions, and switch the toggle in the top right 
4) Click load unpacked and select the folder you put the files
5) Give the extension about 1 minute (depending on your net speed) to download the various files, you can select 'view background page' to access the console in developer mode, and see the various settings. Federated Client is set to Verbose by default.

### Src/
This folder contains all the source files, split by the individual components.
#### Crawler (Document Scraper)
Language: Python
This is the Scrapy package including the relevant files to for the Document Scraper. It is written in Python and should be deployed on a Google App Engine or Compute Engine instance.
If you want to test it locally, you need to go to the Crawler directory and run: `scrapy crawl DocScraper`
#### DD-AdminPanel
Language: C#
This is the Admin Panel for the Application Tier (Service Layer). This is written in C# and requires ASP.NET Core v2.0 to run, and credentials for the DBMS.
#### DDServiceLayerAPI
Language: C#
This is the API for the Application Tier (Service Layer). This is written in C# and requires ASP.NET Core v2.0 to run, and credentials for the DBMS.
#### FederatedClient
Language: NodeJS / Typescript
This is the Application Logic for the Chrome Browser Extension, it corresponds to background.js in the /App/ folder. If you want to build, copy the folder to your local computer and run the below:
`yarn run build` will run all the necessary logic for you.
#### FederatedClientUI
Language: NodeJS / Typescript
This is the Presentation Logic for the Chrome Browser Extension, written with ReactJS. It corresponds to 'federated-ui.js' in the project report, but in reality, it is sharded into many smaller js files in the App/static/js. 
If you download locally, you can run `npm run-script build` and it is advised that you run  `npm install` to ensure dependencies are downloaded.
#### FederatedServer
Language: Python
This is the server-side script for performing the Federated Aggregate, Update, and Model Training. This is designed to be run in a GCP Compute Instance as cronjob, but you can easily run it locally. Pay careful attention to the Config.py before running it as it contains important hyperparameters.
#### Firebase
Language: NodeJS / Typescript
This is a very lightweight NodeJS file that is designed to be deployed in GCP's Firebase app engine, so that it can provide automated counter logic within the Firebase NoSQL document store (there is none built in, which means you need to iterate through the entire collection to count, which is charged per read!)

### Note on Heavy Files
Due to github size restrictions, it was not possible to include the following files in this submission:
* The latest pickled Neural Network model (which is just over 100MB)
* The latest tokenizer (which is over 141MB) for the Federated Server
* The latest tokenizer (which is over 100mb) for the Federated Client

In order to get a copy of the correct Tokenizer, please drop me a note on github, or at ant@inmachine.io
