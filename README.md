THIS PROJECT IS FOR TESTING
here are the clear steps how to do
# Jenkins CI/CD Pipeline for Maven Web Application

This guide walks you through setting up a Jenkins CI/CD pipeline to deploy a Maven-based web application to a Tomcat server. Follow the steps below to configure your environment and automate your deployment process.

## Prerequisites

- **Tomcat 9**: Download and install from [Apache Tomcat](https://tomcat.apache.org/download-90.cgi) 🐱
- **Jenkins**: Download and install from [Jenkins.io](https://www.jenkins.io/download/) ⚙️
- **Maven**: Download and install from [Apache Maven](https://maven.apache.org/download.cgi) 🛠️

## Step 1: Install and Configure Tomcat

1. **Download and Install Tomcat**:
   - Download Tomcat 9 and extract it to your desired location.

2. **Create a Tomcat User with Manager Privileges**:
   - Edit the `tomcat-users.xml` file located in the `conf` directory of your Tomcat installation.
   - Add the following lines to create a user with manager privileges:
     ```xml
     <role rolename="manager-gui"/>
     <user username="admin" password="admin" roles="manager-gui"/>
     ```

3. **Change Tomcat Port to 8081**:
   - Open the `server.xml` file in the `conf` directory.
   - Find the Connector element and change the port attribute to 8081:
     ```xml
     <Connector port="8081" protocol="HTTP/1.1"
                connectionTimeout="20000"
                redirectPort="8443" />
     ```

4. **Start Tomcat**:
   - Navigate to the `bin` directory of your Tomcat installation.
   - Run the `startup.sh` script (on Linux/Mac) or `startup.bat` (on Windows).

## Step 2: Install Jenkins

1. **Download and Install Jenkins**:
   - Download Jenkins and follow the installation instructions for your operating system.

2. **Set Up Jenkins**:
   - Start Jenkins by running `java -jar jenkins.war` from the directory where Jenkins is installed.
   - Access Jenkins at `http://<your-ip>:8080`.
   - Follow the setup wizard to create an admin user and install default plugins.

## Step 3: Configure Jenkins for Maven and GitHub

1. **Install Maven Plugin**:
   - Go to `Manage Jenkins` > `Manage Plugins`.
   - Install the Maven Integration plugin.

2. **Install Deploy to Container Plugin**:
   - Go to `Manage Jenkins` > `Manage Plugins`.
   - Install the Deploy to Container plugin.

## Step 4: Create a Jenkins Job for Your Project

1. **Create a New Item**:
   - Click on `New Item`.
   - Enter a name for your project and select `Freestyle project`.
   - Click `OK`.

2. **Configure the Job**:
   - **General**:
     - Enter a description for your project.
   
   - **Source Code Management**:
     - Select `Git`.
     - Enter your GitHub repository URL.

   - **Build Triggers**:
     - Select `Poll SCM`.
     - Set the schedule (e.g., `H/5 * * * *` to poll every 5 minutes).

   - **Build Steps**:
     - Add a build step and select `Invoke top-level Maven targets`.
     - Set the Maven version and goals (e.g., `clean install`).

   - **Post-build Actions**:
     - Add a post-build action and select `Deploy war/ear to a container`.
     - Set the WAR/EAR files location (e.g., `/target/*.war`).
     - Set the context path (e.g., `/`).
     - Add a container and configure it to deploy to your Tomcat server running on port 8081.

3. **Save the Job**:
   - Click `Save`.

## Step 5: Run the Job

1. **Build the Project**:
   - Click on `Build Now` to start the build process.

2. **Monitor the Build**:
   - Check the build progress and logs to ensure everything is running smoothly.

3. **Verify Deployment**:
   - Access your application at `http://<your-ip>:8081/<context-path>` to verify the deployment.

This process will help you set up a Jenkins CI/CD pipeline to deploy a Maven-based web application to Tomcat. If you encounter any issues, feel free to ask for help!
