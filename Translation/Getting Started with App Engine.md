# Google Cloud Fundamentals: Getting Started with App Engine

## Objectives:
 In this lab, you learn how to perform the following tasks:

    -Initialize App Engine.
    -Preview an App Engine application running locally in Cloud Shell
    -Deploy an App Engine application, so that others can reach it.
    -Disable an App Engine application, when you no longer want it to be visible.
    -Set up your lab environment
  
## Steps:

1. Sign in to the Google Cloud Platform (GCP) Console

2. In GCP console, on the top right toolbar, click the Open Cloud Shell button.

3. Initialize your App Engine app with your project and choose its region using this command:
    ```
      gcloud app create --project=$DEVSHELL_PROJECT_ID
	```
	- When prompted, select the region where you want your App Engine application located. (for this lab select us-central1)

4. Clone the source code repository for a sample application in the hello_world directory:
    ```
	git clone https://github.com/GoogleCloudPlatform/python-docs-samples
	```
		 
5. To navigate to the source directory use the following command:
    ```
	cd python-docs-samples/appengine/standard_python3/hello_world
	```

Run Hello World application 

6. Execute the following command to download and update the packages list.
	```
	sudo apt-get update
	```
        		
7. Set up a virtual environment in which you will run your application locally before deploying.
	```
	sudo apt-get install virtualenv
	```
    
	If prompted [Y/n], press Y and then Enter.

8. Run the following command to setup the files required to run virtualenv on python 3
	```
	virtualenv -p python3 venv
	```
   
9. Activate the virtual environment. 
	```
	source venv/bin/activate
	```
      
10. Navigate to your project directory and install dependencies for project listed in requirements.txt
	```
	pip install  -r requirements.txt
	```
    
11. To Run the application:
	```
	python main.py
	```
    
12. Preview the app on localhost:8080 and then quit when done. (In Cloud Shell, click Web preview (Web Preview) > Preview on port 8080 to preview the application)

13. End the test, return to Cloud Shell and press Ctrl+C to abort the deployed service.


Deploy and run Hello World on App Engine

14. Navigate to the source directory:
	```
	cd ~/python-docs-samples/appengine/standard_python3/hello_world
	```
        
15. Deploy your Hello World application.
	```
	gcloud app deploy
	```

	If prompted "Do you want to continue (Y/n)?", press Y and then Enter.

16. Run this command to view your application link and visit app. Launch your browser to view the app at http://YOUR_PROJECT_ID.appspot.com
	```
	gcloud app browse
	```

	Copy and paste the URL into a new browser window to view the results.


17. Disable the application

	App Engine offers no option to Undeploy an application. After an application is deployed, it remains deployed, However, you can disable the application, which causes it to no longer be accessible to users. To do this you have to navigate to the cloud shell and then disable the application.

	In the cloud shell type the folowwing command to open the console
	```
	gcloud app open-console
	```
	
	a link will appear and use it to navigate to the app engine settings and disable the application

