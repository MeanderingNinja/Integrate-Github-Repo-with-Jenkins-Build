# Integrate-Github-repo-with-Jenkins-build
This documentation is to showcase how I integrate a github repo with a Jenkins job for my CICD pipeline. 

### Set up a webhook in your GitHub repository that points to your Jenkins instance
- Go to your GitHub repository and click on **"Settings"**
- Then, click on **"Webhooks"** and click the **"Add webhook"** button.
- Enter the **Payload URL** of your Jenkins instance and set the **content type** to **"application/json"**.
- Select the events you want to trigger the webhook, such as "Pushes" for code changes, and save the webhook.

*Note*: 
1. *A **payload URL** is the URL of a web service or API endpoint that receives incoming data from a webhook. In this case, a payload URL for a webhook that is set up to trigger a Jenkins build would be the URL of the Jenkins server followed by the path to the Jenkins job that you want to trigger.*
2. *Since I set up a Jenkins server locally, I exposed it to the public using the [ngrok](https://www.youtube.com/watch?v=yMNJeWeE0qI) utility. The ngrok-generated forward public IP address suffixed with`/github-webhook/` is the payload URL I used in the Github Webhook setting.* Without the suffix, Github won't be able to POST to the Jenkins server successfully. This is most likely due to Jenkins only allowing requests from a specific URL path. 
  
### Configuring the Jenkins project that I want to build a trigger for when code changes
- In Jenkins, click on "**Configure**" for the project, and go to the "**Build Triggers**" section.
- Check the "**GitHub hook trigger for GITScm polling**" checkbox. This will enable the Jenkins project to automatically poll your GitHub repository for code changes and trigger a build if there are any.
- Save the configuration changes.
Now, whenever there is a code change in my GitHub repository, Jenkins should automatically trigger a build in response to the code change.


