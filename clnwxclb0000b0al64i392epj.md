---
title: "A Comprehensive Guide to Integrating Slack with Jenkins"
datePublished: Thu Oct 19 2023 08:32:52 GMT+0000 (Coordinated Universal Time)
cuid: clnwxclb0000b0al64i392epj
slug: a-comprehensive-guide-to-integrating-slack-with-jenkins
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697704279132/597f5c68-ec52-4349-bba1-d25f668c7090.png
tags: blogging, aws, slack, devops, integration

---

In the dynamic landscape of modern software development, effective communication and teamwork are paramount. Picture yourself immersed in a software project, with the need to maintain constant team updates throughout the development journey.

This is precisely where the synergy between Slack, the renowned messaging platform, and Jenkins, the automation juggernaut, takes center stage. By integrating Slack with Jenkins, you unlock the potential for receiving real-time notifications and progress reports all in one consolidated hub.

In this article, we’ll delve into the harmonious fusion of these two tools, promising to elevate your software development process into a more efficient and enjoyable experience. Let’s embark on this enlightening journey!

![](https://miro.medium.com/v2/resize:fit:875/0*hFb1jEKUfh2XvV-G align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*bmhAZ6sFFQGi-Mfv align="left")

# **STEPS:**

Step 1: Create a Slack account

Step 2: Launch an ec2 instance and install Jenkins on it.

Step 3: Install the Jenkins CI app on Slack

Step 4: Install the Splunk Notification Plugin on Jenkins

Step 5: Run a Sample test

# **Create a Slack account**

* Open your preferred web browser (e.g., Google Chrome, Mozilla Firefox, Safari, or Microsoft Edge).
    
* In the address bar, type or click on the following URL to access Slack’s official website: [https://slack.com](https://slack.com)
    
* On the Slack homepage, you’ll find a prominent “SIGN UP WITH GOOGLE” or “Try for Free” button. Click on it.
    

![](https://miro.medium.com/v2/resize:fit:875/1*g1ja7LNMoISq5-RMsI17NA.png align="left")

* Select your mail here to create an Account
    

![](https://miro.medium.com/v2/resize:fit:875/1*HOrwIv-_z3aHHxgAcTj_4g.png align="left")

* Sometimes it may ask for the password of your mail, or it will move to the next page
    
* confirm your mail
    
* Now click on Create a Workspace.
    

![](https://miro.medium.com/v2/resize:fit:875/1*Ga-W-3cT1zDCv0ZQs-5esw.png align="left")

* Provide a name for your Slack and click next
    

![](https://miro.medium.com/v2/resize:fit:875/1*4KBgAOGeukDoSCxOPxQTEA.png align="left")

* Next, provide your name that helps your teammates recognise and add a profile photo
    

![](https://miro.medium.com/v2/resize:fit:875/1*zR36JPTaJCLEmY3-_E3IPQ.png align="left")

* If you want to add your friends to the Slack channel provide their email or send an invitation. otherwise, skip
    

![](https://miro.medium.com/v2/resize:fit:875/1*PCBe626EzdIk7ghxy3Cajw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*zeIUiddFlFl24QBOLrRORg.png align="left")

* We are using Slack for Jenkins right that’s why I provided the name Jenkins and clicked on the next
    

![](https://miro.medium.com/v2/resize:fit:875/1*g8Z-vWQKr_T8wUQC40iAVQ.png align="left")

* Now Slack created a channel named Jenkins and clicked Let’s Go.
    

![](https://miro.medium.com/v2/resize:fit:875/1*4mEaRiY61A_d84-uDBI8Sg.png align="left")

* Your Slack account has been created. Now you can send messages
    

![](https://miro.medium.com/v2/resize:fit:875/1*v83pWc2SRcEt0ZKFh0miIg.png align="left")

# **Launch Ec2 Instance with Jenkins**

* Launch an Ubuntu ec2 instance in the AWS console and use the below user data to install Jenkins on it
    

```plaintext
#!/bin/bash

# Update the package list
sudo apt update -y

# Add Adoptium repository key
wget -O - https://packages.adoptium.net/artifactory/api/gpg/key/public | sudo tee /usr/share/keyrings/adoptium-archive-keyring.gpg > /dev/null

# Add Adoptium repository to sources list
echo "deb [signed-by=/usr/share/keyrings/adoptium-archive-keyring.gpg] https://packages.adoptium.net/artifactory/deb $(awk -F= '/^VERSION_CODENAME/{print$2}' /etc/os-release) main" | sudo tee /etc/apt/sources.list.d/adoptium.list

# Update package list again
sudo apt update -y

# Install Temurin (formerly AdoptOpenJDK) 17 JDK
sudo apt install temurin-17-jdk -y

# Check Java version
/usr/bin/java --version

# Add Jenkins repository key
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo gpg --dearmor -o /usr/share/keyrings/jenkins-archive-keyring.gpg

# Add Jenkins repository to sources list
echo "deb [signed-by=/usr/share/keyrings/jenkins-archive-keyring.gpg] https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list

# Update package list
sudo apt update -y

# Install Jenkins
sudo apt-get install jenkins -y

# Start Jenkins service
sudo systemctl start jenkins

# Check Jenkins service status
sudo systemctl status jenkins

# Display the initialAdminPassword
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

* This will install Jenkins on it. and install suggested plugins and create a user for Jenkins.
    

# **Install the Jenkins CI app on Slack**

* Go to Slack and click on your name
    
* Select Settings and Administration
    
* Click on Manage apps
    

![](https://miro.medium.com/v2/resize:fit:875/1*FbhimJKa6FDs_ghW8_bUNQ.png align="left")

* It will open a new tab
    
* Search for Jenkins CI and click on it
    

![](https://miro.medium.com/v2/resize:fit:875/1*rm6rHFxk702kszl1zalYdQ.png align="left")

* It will open another tab
    
* Click on Add to Slack
    

![](https://miro.medium.com/v2/resize:fit:875/1*U3u7rTqJiR1cUWyWyiPZqg.png align="left")

* Now choose your Slack channel
    
* Click on Add Jenkins CI integration.
    

![](https://miro.medium.com/v2/resize:fit:875/1*4q1WClMGA81kbon5wDXu8Q.png align="left")

* You will be redirected to this page
    

![](https://miro.medium.com/v2/resize:fit:875/1*lDoFKW5ErlQe_KUYYWXjrQ.png align="left")

* Copy the team subdomain and integration token credential ID for later use.
    

![](https://miro.medium.com/v2/resize:fit:875/1*mj1oJx6XOTa7yq8o8bb4hA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*sI8jN86dXRoBF846YsYMFA.png align="left")

# **Install Slack Notification Plugin in Jenkins**

* Go to Jenkins Dashboard
    
* Click on manage Jenkins → Plugins → Available plugins
    
* Search for Slack Notification and install
    

![](https://miro.medium.com/v2/resize:fit:875/1*bM-x6yTnbWpOIIxiMR6iWw.png align="left")

* Click on Manage Jenkins → Credentials → Global
    
* Select kind as Secret Text
    
* At Secret Section Provide Your Slack integration token credential ID
    
* Id and description are optional and create
    

![](https://miro.medium.com/v2/resize:fit:875/1*mj1oJx6XOTa7yq8o8bb4hA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*r3CieFnBDiXdKQ0in7LYeA.png align="left")

* Click on Manage Jenkins → System
    
* Go to the end of the page
    
* Workspace → team subdomain
    
* Credential → Select your Credential for Slack
    
* Default channel → Provide your Channel name
    
* Test connection
    

![](https://miro.medium.com/v2/resize:fit:875/1*mj1oJx6XOTa7yq8o8bb4hA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*6u7X8rN8XeBA6DNVbvfrmQ.png align="left")

* Click on Apply and save
    
* Now Go to Jenkins Dashboard click on New item or create a Pipeline job
    
* and add this pipeline
    

```plaintext
def COLOR_MAP = [
    'FAILURE' : 'danger',
    'SUCCESS' : 'good'
]

pipeline {
    agent any
    stages {
        stage('Hello') {
            steps {
                echo "Hello world"
            }
        }
    }
    post {
        always {
            script {
                def slackColor = COLOR_MAP[currentBuild.currentResult] ?: 'warning' // Default to 'warning' if the result is not explicitly defined

                echo 'Sending Slack Notifications'

                slackSend(
                    channel: '#channel-name', // Change your channel name
                    color: slackColor,
                    message: """
                    *${currentBuild.currentResult}:* Job ${env.JOB_NAME}
                    build ${env.BUILD_NUMBER}
                    More info at: ${env.BUILD_URL}
                    """
                )
            }
        }
    }
}
```

![](https://miro.medium.com/v2/resize:fit:875/1*23qoz4m-BLXUWUtzBpLUbw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*oz6Z6h6EZpbWmZiYXZNavA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*e6lnegLBKF8JLAHWE4POvQ.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*x5wV0DBU_o4WoWfBByF-Zg.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*YbE0RGm53wtzSSP3yUSCAw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*CTHkwaeVxf8p60zk8QmsCw.png align="left")

* You will get a Notification in Slack
    

![](https://miro.medium.com/v2/resize:fit:875/1*uPxwZb7OfKUqAdERSl5ySw.png align="left")

Slack and Jenkins, each a formidable asset in your DevOps arsenal, can unleash their full potential when they collaborate. Together, they open up a realm of limitless possibilities, providing real-time notifications, streamlining communication, and fostering seamless teamwork. This union isn’t just a connection; it’s a bridge that seamlessly melds the worlds of messaging and automation.

Your feedback is instrumental to our growth, so please feel free to reach out to me on LinkedIn at [Mudit Mathur](https://www.linkedin.com/in/mudit--mathur/) ([https://www.linkedin.com/in/mudit--mathur/](https://www.linkedin.com/in/mudit--mathur/)). Stay tuned for a continuous stream of invaluable DevOps insights, along with an ever-evolving treasure trove of tips and tricks. As we journey forward, your support and curiosity are deeply appreciated.

Thank you for being a part of my blog’s readership.