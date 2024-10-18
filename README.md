### Tools to Install:

* Docker
* Docker Compose

### Step 1: Install Jenkins Using Docker Compose
**Create a directory for Jenkins:**
* mkdir jenkins-docker
* cd jenkins-docker

**Create a docker-compose.yml file:**

**Start Jenkins**
* docker-compose up -d

**Access Jenkins**
***http://localhost:8080. To unlock Jenkins, follow the steps provided on the initial screen to retrieve the admin password:***
* docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword

### Step 2: Create a Dockerfile for the Website
**Create a project directory**
* mkdir t2s-website && cd t2s-website

**Create a simple HTML file**

**Create a Dockerfile**

**Build the Docker image**
* docker build -t t2s-website .

**Run the container**
* docker run -d -p 80:80 t2s-website

### Step 3: Push the Code to GitHub
**Initialize Git in your project directory**
* git init
* git branch -M main
* git remote add origin https://github.com/Here2ServeU/jenkins-github-docker.git

**Add the files and push to GitHub**
* git add .
* git commit -m "Add Dockerfile and website"
* git push -u origin main

### Step 4: Create a Webhook with Jenkins
**Install “GitHub” Plugin in Jenkins**
* Go to Manage Jenkins -> Manage Plugins -> Available and search for “GitHub Plugin.”
* Install the plugin and restart Jenkins if necessary.

**Create a Jenkins Job**
* Go to New Item, select Freestyle project, and configure it.
* Under the Source Code Management section, select Git and enter your repository URL.
* Under Build Triggers, select GitHub hook trigger for GITScm polling.

**Configure Webhook in GitHub**
* Go to your GitHub repository -> Settings -> Webhooks -> Add webhook.
* In the Payload URL, enter your Jenkins URL followed by /github-webhook/ (e.g., http://your-jenkins-url/github-webhook/).
* Set the Content type to application/json and ensure Just the push event is selected.

**Test the Webhook**
* Push changes to your repository, and Jenkins should automatically trigger the build.