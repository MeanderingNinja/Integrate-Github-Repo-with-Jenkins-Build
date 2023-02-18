# How to Integrate a Github Repo With a Jenkins Build
This documentation is to showcase how I integrated a github repo with a Jenkins job for my CICD pipeline. 
## Setup 
- The Jenkins Server Version: 2.375.3(Installed locally on a Ubuntu machine)
- Github Repo Used: https://github.com/emma-jinger/cat_data (A Jenkinsfile is included in the repo)

### Step 1: Generating a token for Jenkins on Github 

### Step 2: Setting up a webhook in your GitHub repository that points to your Jenkins instance
- Go to your GitHub repository and click on **"Settings"**
- Then, click on **"Webhooks"** and click the **"Add webhook"** button.
- Enter the **Payload URL** of your Jenkins instance and set the **content type** to **"application/json"**.
- Select the events you want to trigger the webhook, such as "Pushes" for code changes, and save the webhook.

*Note*: 
1. *A **payload URL** is the URL of a web service or API endpoint that receives incoming data from a webhook. In this case, a payload URL for a webhook that is set up to trigger a Jenkins build would be the URL of the Jenkins server followed by the path to the Jenkins job that you want to trigger.*
2. *Since I set up a Jenkins server locally, I exposed it to the public using the [ngrok](https://www.youtube.com/watch?v=yMNJeWeE0qI) utility. The ngrok-generated forward public IP address suffixed with`/github-webhook/` is the payload URL I used in the Github Webhook setting.* Without the suffix, Github won't be able to POST to the Jenkins server successfully. This is most likely due to Jenkins only allowing requests from a specific URL path. 
3. *I am using the free version of ngrok, so every time ngrok restarts, the forward IP is different. Modify settings accordingly for testing.*



### Step 3: Configuring Jenkins
* Install the **Github plugin** in "Manage Jenkins" -> "Manage Plugins".
* Add the Github server in "Manage Jenkins" -> "Configure System" -> "Github"
  * Click the "**Add**" button to add a new GitHub server.
  * In the "GitHub Server" section, enter a name for the server, and the API URL for your GitHub instance (e.g., <ins>https://api.github.com</ins>).
  * Enter personal access token (generated in GitHub that has the "repo" scope) in the "**Credentials**" section.
  * Click "**Test Connection**" to verify that Jenkins can connect to your GitHub instance.
  * Check the "Manage Hooks" field
  * Click "Save" to save the configuration.


*Note:* 
*1. The github plugin allows Jenkins to receive notifications from GitHub when code changes occur, and trigger builds or other actions in response.*
*2. The "Manage Hooks" field allows you to configure Jenkins to automatically create and manage webhook URLs for your GitHub repositories. If this option is selected, Jenkins will automatically create webhook URLs for each repository that you add to a Jenkins job.*  

### Step 4: Configuring the Jenkins project that I want to build a trigger for when code changes
- In Jenkins, click on "**Configure**" for the project, and go to the "**Build Triggers**" section.
- Check the "**GitHub hook trigger for GITScm polling**" checkbox. This will enable the Jenkins project to automatically poll your GitHub repository for code changes and trigger a build if there are any.
- Save the configuration changes.

Now, whenever there is a code change in my GitHub repository, Jenkins should automatically trigger a build in response to the code change.


