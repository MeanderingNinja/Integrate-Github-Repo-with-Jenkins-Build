# Integrate-Github-repo-with-Jenkins-build
This documentation is to showcase how I integrate a github repo with a Jenkins job for my CICD pipeline. 

### Ensure that you have set up a webhook in your GitHub repository that points to your Jenkins instance.
- Go to your GitHub repository and click on "Settings"
- Then, click on "Webhooks" and click the "Add webhook" button.
- Enter the Payload URL of your Jenkins instance and set the content type to "application/json".
- Select the events you want to trigger the webhook, such as "Pushes" for code changes, and save the webhook.
### Configuring the Jenkins project that I want to build a trigger for when code changes
- In Jenkins, click on "**Configure**" for the project, and go to the "**Build Triggers**" section.
- Check the "**GitHub hook trigger for GITScm polling**" checkbox. This will enable the Jenkins project to automatically poll your GitHub repository for code changes and trigger a build if there are any.
- Save the configuration changes.
Now, whenever there is a code change in my GitHub repository, Jenkins should automatically trigger a build in response to the code change.


