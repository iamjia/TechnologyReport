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

* [Continuous Integration and Delivery for iOS with Jenkins and Fastlane (Part 1)](https://medium.com/@cherrmann.com/continuous-integration-and-delivery-for-ios-with-jenkins-and-fastlane-part-1-3b17f1901a73)


## Install Tomcat + java runtime

* [Installing Tomcat on macOS 10.14 Mojave](https://wolfpaulus.com/mac/tomcat/)

* [JDK management between versions](https://docs.oracle.com/javase/8/docs/technotes/guides/install/mac_jdk.html#A1096903)


## Install Jenkins and launch in Tomcat

* [Download Jenkins .war package](https://jenkins.io)

* Copy `jenkins.war` into `webapp` directory in Tomcat's home directory

* Launch Tomcat server and visit [http://localhost:8080/jenkins](http://localhost:8080/jenkins)



## Configure Jenkins and Install plugins

### Configure Global Security and set up your account of Jenkins.


### Plugins to install

Developer tool

* [Xcode integration](https://wiki.jenkins.io/display/JENKINS/Xcode+Plugin)

* [Keychains and Provisioning Profiles Management](Keychains and Provisioning Profiles Management)


Code repository

* [GitLab](https://wiki.jenkins-ci.org/display/JENKINS/GitLab+Plugin)

* [Gitlab Hook Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Gitlab+Hook+Plugin)

* [Gitlab Merge Request Builder](https://wiki.jenkins-ci.org/display/JENKINS/Gitlab+Merge+Request+Builder+Plugin)


Build control

* [Commit Message Trigger Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Commit+Message+Trigger+Plugin)

* [Email Extension Template](https://wiki.jenkins-ci.org/display/JENKINS/Email-ext+Template+Plugin)

* [build-name-setter](http://wiki.jenkins-ci.org/display/JENKINS/Build+Name+Setter+Plugin)

* [Environment Injector](https://wiki.jenkins-ci.org/display/JENKINS/EnvInject+Plugin)



## Reference
