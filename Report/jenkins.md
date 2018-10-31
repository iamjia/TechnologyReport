# macOS + Tomcat + Jenkins + fir.im

* iOS Continous integration with Jenkins

	* code review CI

	* daily build CI

	* ci build CD

* Distribute ipa files with fir.im

* Manage Jenkins server with ssh 



## Why Jenkins

* [iOS Continous integration: Xcode Server, Jenkins, Travis and fastlane](http://thebugcode.github.io/ios-continous-integration-choosing-a-build-server-and-tooling/)

* [IOS CONTINUOUS INTEGRATION WITH FASTLANE & JENKINS](https://apiumhub.com/tech-blog-barcelona/ios-continuous-integration/)


## Install Tomcat + java runtime

* [Installing Tomcat on macOS 10.14 Mojave](https://wolfpaulus.com/mac/tomcat/)

* [JDK management between versions](https://docs.oracle.com/javase/8/docs/technotes/guides/install/mac_jdk.html#A1096903)

We will use JDK for java 8 here, since java 11 has not widely supported by Jenkins and its plugins.
 

## Install Jenkins and launch in Tomcat

* [Download Jenkins .war package](https://jenkins.io)

* Copy `jenkins.war` into `webapp` directory in Tomcat's home directory

* Launch Tomcat server and visit [http://localhost:8080/jenkins](http://localhost:8080/jenkins)



## Configure Jenkins and Install plugins

1. [Continuous Integration and Delivery for iOS with Jenkins and Fastlane (Part 1)](https://medium.com/@cherrmann.com/continuous-integration-and-delivery-for-ios-with-jenkins-and-fastlane-part-1-3b17f1901a73)

2. Configure Global Security and set up your account of Jenkins.

3. Set system admin email in `System Preferences`: which will be used to send mails.

* Configure `E-mail Notification`

* Configure `Extended E-mail Notification`
	
Configure SMTP server of your email and test connections.


### Jenkins plugins to install

Developer tool

* [Xcode integration](https://wiki.jenkins.io/display/JENKINS/Xcode+Plugin)

* [Keychains and Provisioning Profiles Management](Keychains and Provisioning Profiles Management)


Code repository

* [Gerrit Trigger](http://wiki.jenkins-ci.org/display/JENKINS/Gerrit+Trigger)

* [GitLab](https://wiki.jenkins-ci.org/display/JENKINS/GitLab+Plugin)

* [Gitlab Hook Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Gitlab+Hook+Plugin)

* [Gitlab Merge Request Builder](https://wiki.jenkins-ci.org/display/JENKINS/Gitlab+Merge+Request+Builder+Plugin)


Build control

* [Commit Message Trigger Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Commit+Message+Trigger+Plugin)

* [Email Extension Template](https://wiki.jenkins-ci.org/display/JENKINS/Email-ext+Template+Plugin)

* [build-name-setter](http://wiki.jenkins-ci.org/display/JENKINS/Build+Name+Setter+Plugin)

* [Environment Injector](https://wiki.jenkins-ci.org/display/JENKINS/EnvInject+Plugin)


#### Configure Jenkins plugins

Go to `Manage Jenkins`

1. Gerrit Trigger > Add New Server > Named like `XXGerrit`

 Fillup the basic information and `SSH Keyfile`.


2. Editable Email Notification Templates > Add New Template

* iOS code review template

* iOS ci build template


Configure `Default Content`, `Advanced Settings` of your templates by different purpose.

*Plenty of variables will help your template contents configuration. You can even inject your own variables outside, such as git change logs.*


3. Keychains and Provisioning Profiles Management



### Create your Jenkins jobs

1. Set a display name for job if a human readable name is necessary

2. Add your git repo `Source Code`

* Check on `Recursively update submodules` in `Additional Behaviours` if you used `git submodule`
  
* Add `Additional Behaviours` in `Source Code`: `Gerrit Trigger`

3. Build trigger
   
* Gerrit Trigger
	* Choose your gerrit server added above `XXGerrit`

4. Build environment


#### Code review CI job


* GitLab


#### Daily build CI job


#### CI build CD job

* Gerrit Trigger
	* Add `Trigger on`: `Change Merged`


## Reference
