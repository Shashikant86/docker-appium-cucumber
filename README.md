# Cucumber : Docker Setup for Appium-Android

Repository for automated builds of appium server container. This container can be used as jenkins-slave for your automated tests using Ruby Cucumber.

# Software included
- Ruby 2.0
- RVM
- Bundler
- BDDfire
- Maven3
- jdk8
- appium 1.4.10
- android android-sdk_r24.1.2
- android build-tools-22.0.1

# Starting Appium Server
## Just 1 appium server
Run container with usb privileges to find the phisical device
```
$ docker run -d --privileged -v /dev/bus/usb:/dev/bus/usb  -p 4723:4723 shashikant86/docker-appium-cucumber
```
## More than 1 appium server
Start 2 appium servers with diferents configurations. [Check appium Doc.](https://github.com/appium/appium/blob/master/docs/en/appium-setup/parallel_tests.md)
- '-p' port: the main Appium port
- '-bp' bootstrap port: the device id
- '-U' UDID: the Appium bootstrap port

```
$ docker run -d --privileged -v /dev/bus/usb:/dev/bus/usb -e appium_args="-p 4723 -bp 2251 -U 32456"  -p 4723:4723 shashikant86/docker-appium-cucumber

$ docker run -d --privileged -v /dev/bus/usb:/dev/bus/usb -e appium_args="-p 4724 -bp 2252 -U 43364" -p 4724:4724 shashikant86/docker-appium-cucumber

```

# Running Cucumber Tests

Once you have started container.

* Check Appium version

             $ docker exec CONTAINER_ID appium -v


* Check cucumber version

             $ docker exec CONTAINER_ID /bin/bash -l -c "cucumber -v"


* Run Cucumber tests with headless driver Poltergeist

             $ docker exec bc6aba5d09a4 /bin/bash -l -c "cd cucumber&&bundle exec rake parallel_cucumber"

* Run Cucumber tests with headless driver Poltergeist

            $ docker exec bc6aba5d09a4 /bin/bash -l -c "cd cucumber&&bundle exec cucumber -p appium_android_web ADB_SERIAL=your_serial"
