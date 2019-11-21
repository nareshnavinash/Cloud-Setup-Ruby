# Cloud Automation Setup

To run web automation suites in the Jenkins, we need to ensure that the following items are preinstalled in the Linux & Jenkins server.

1. Need to have Ruby and RVM.
2. Need to have Bundler gem installed.
3. Need to have the required browsers in which automation suites are going to run. (eg., Chrome, Firefox, etc.,)
4. Need to have (Selenium) Drivers corresponding to the browsers. (When Selenium 4.0+ is released this drivers is need not to be installed separately, since it will have internal driver manager.)
5. Each Jenkins slave (where UI automation is running) should have minimum 2GB ram and minimum 2 core processor with 1.2GHZ processor.
6. Allure plugin to be added in Jenkins (For reporting purpose)


Installation Procedures: (may change over a period of time)

## Ruby: 2.5.3

https://www.ruby-lang.org/en/documentation/installation/

gem install bundler



## RVM:

https://rvm.io/rvm/install



## Browsers:

### Chrome Installation:
The following will install latest chrome in linux
```
sudo apt-get install google-chrome-stable
```

### Uninstall Chrome:
```
sudo apt-get purge google-chrome-stable
rm ~/.config/google-chrome/ -rf
```

### Install Chrome with specific version:
```
wget https://repo.aosc.io/debs/pool/stable/main/g/google-chrome_78.0.3904.70-0_amd64.deb # URL to download the deb file
sudo dpkg -i google-chrome_78.0.3904.70-0_amd64.deb # name of the downloaded deb file
sudo apt-get -f install # To resolve the installation with dependencies
```


## Browser Drivers:

### Install Chrome driver:
```
version=$(curl -s https://chromedriver.storage.googleapis.com/LATEST_RELEASE)
wget -qP "/tmp/" "https://chromedriver.storage.googleapis.com/${version}/chromedriver_linux64.zip"
sudo unzip -o /tmp/chromedriver_linux64.zip -d /home/ubuntu/.rvm/gems/ruby-2.5.1/wrappers/chromedriver # in which ever location you want
sudo chmod 755 /usr/bin/chromedriver
sudo chown root:root /usr/bin/chromedriver
sudo chmod +x /usr/bin/chromedriver
```

### Uninstalling chrome driver:
```
find / -name "chromedriver"
sudo rm -rf /usr/bin/chromedriver # remove all the paths listed in the above command
chromedriver -v # should not give any versions
```


## Allure for jenkins:

https://www.wedoqa.com/2017/11/allure-integration-in-jenkins/



## Plugins for Jenkins

https://wiki.jenkins.io/display/JENKINS/Rebuild+Plugin

https://jenkins.io/doc/pipeline/steps/allure-jenkins-plugin/

## In the shell prompt in jenkins

Add the following to use the ruby in shell prompt and then run.
```
#!/bin/bash -l
rvm list
ls
cd <path_to_the_project>
cucumber #or custom commands
```

## In Jenkins allure plugin configuration

In the results path give `**/<path_to_your_allure_generated_folder>/` path to the allure.
Set the report path and allure configuration as `allure-report`.
