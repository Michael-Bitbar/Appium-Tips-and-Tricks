# Appium Tips & Tricks
Bitbar supports thousands of customers that are using Appium in on Bitbar Test Cloud, Bitbar Private Cloud as well as Bitbar On-Premise systems. The Bitbar  Professional Services team also helps jump start test automation, maintains test automation frameworks or even manages end-to-end testing for customers. I've been closely involved in supporting customers that want to run Appium on Bitbar Test Cloud and I wanted to share some general tips & tricks to help people adopt Appium into their test process.

## Testing Facebook Login Integration

The Facebook SDK enables people to sign into apps with Facebook Login. When people log into an app with Facebook they can grant permissions to it, so you can retrieve information or perform actions on Facebook on their behalf.

Useful, right? Yea, only when it works! How the heck do you test this integration with your app across a large spectrum of mobile devices that may present the login screen differently, depending on the OS version? The good news is, Facebook is already installed by the OEM on a lot of devices. The bad news is, there are a couple different scenarios you have to take into consideration when planning out your mobile test automation framework:

1. Android 4.4+
2. Older Android versions

Note: If a device has the native Facebook app installed, it will be used by default and will remove the access token, so that user will not stay logged in.

## Desired Capabilities for Bitbar Test Cloud
Includes versions for client-side and server-side execution.

Desired capabilities are a set of keys and values sent to the Appium server to tell the server what kind of automation session should be started. There are also various capabilities to modify the behavior of the server during automation. For example the platformName capability can be set to ‘iOS’ to tell Appium an iOS session is needed, rather than an Android one. Or the safariAllowPopups capability can be set to true in order to ensure that, during a Safari automation session, JavaScript is allowed to open up new windows.

Appium is very similar to Selenium. An Appium test is very similar as a Selenium test: Both use the same WebDriver, and DesiredCapabilities is used the same way. Configuring an application to run on Appium has a lot of similarities to Selenium — for example, those DesiredCapabilities.

To take advantage of Bitbar Testing infrastructure, devices and testing capabilities, additional Desired Capabilities have been introduced. When running Appium tests from client-side some of these desired capabilities are mandatory and some not:

## testdroid_username
Mandatory: yes  
Description: The email registered at Bitbar Testing  
Example: username@domain.com  
Java: capabilities.SetCapability("testdroid_testTimeout", 1200)

## testdroid_password
Mandatory: yes  
Description: The password for your Bitbar Testing account  

## testdroid_target
Mandatory: yes  
Description: The target test type. Use one of the following value. 'android' and 'ios' are for native apps, 'selendroid' when testing a hybrid app and 'chrome' and 'safari' for web testing using the respective web browsers. 'selendroid' is also needed for older devices with API strictly lower than 17.  
Values: android | selendroid | ios | chrome | safari  

## testdroid_project
Mandatory: yes  
Description: The project name that will be displayed on Web UI. See FAQs for more details.  
Example: Appium iOS Project  

## testdroid_description
Mandatory: no  
Description: Project description.  
Example: "My first Appium project at Bitbar Testing cloud"  

## testdroid_testrun
Mandatory: yes  
Description: The name given to each Test Run under a Project. See FAQs for more details.  
Example: Test Run 1  

## testdroid_device
Mandatory: yes  
Description: The device name that uniquely identifies a device on Bitbar Testing cloud. (Copy the name from Web UI, as shown in the snapshot). Alternatively you can use a script to query for devices with particular properties (eg. with a python example).
Example: iPhone 5c 7.0.4 A1532  

## testdroid_app
Mandatory: yes - when not using "browserName" capability for browser automation  
Description: Specifies the Application file (.app/.apk) that would be installed on the device. The App can be given as a public URL, or the SessionId received on uploading the application to Bitbar Testing cloud. For an example on uploading App to Cloud see section this Python example.  
Example: http://www.example.com/MyApp.ipa  
Example: "abcdefg-1234-5678-abcd-111122223333/BitbarIOSSample.ipa"  
Example: "latest" - This option will use the latest apk/ipa uploaded to the selected project. Upload needs to  be done from UI for "latest" to work.  

## testdroid_locale
Mandatory: no  
Description: Device language, identified by java.util.locale Locale ID  
Default: EN  
Example: fi_FI  

## testdroid_junitWaitTime
Mandatory: no  
Description: The time Cloud will wait anticipating a JUnit XML upload after receiving driver.quit()  
Default: 0  
Legal range: 0~300  
Example: 120  

## testdroid_testTimeout
Mandatory: no  
Description: The timeout for whole test execution (in seconds). It's configurable only, if you have active plan/subscription  
Default: 600  
Example: 1200  

## testdroid_apiKey
Mandatory: no  
Description: You can use API key to authentication instead of user name and password. This is available in "My Accounts" -view.  
Default: none  
Example: e4f86ac5b94e39810f33ad4ab71850a6  

## testdroid_testrunId
Scope: Private Cloud & Enterprise only  
Mandatory: no  
Description: You can add a new Appium run as a new device run to an existing testrun by providing a testrunid. Note! New testrun is created, if there's already a run for similar device.  
Default: none  
Example: 12345678  

## testdroid_forceRetryDeviceModel
Scope: Private Cloud & Enterprise only  
Mandatory: no  
Description: This is used with testdroid_testrunId -capability. Bitbar Testing will replace the device run data of an existing device run, if one for the same device model is found.  
Default: false  
Example: true  

## testdroid_findDevice
Scope: Public, Private and Enterprise  
Mandatory: no  
Description: This can be used to turn off Appium client's feature of finding a close match to request device. This allows the requested device name to not be a perfect match but Appium client will search for a similar device.  
Default: true  
Example: false  

## testdroid_gamebench
Scope: Public, Private and Enterprise  
Mandatory: no  
Description: This can be used to turn on/off collecting performance data with Gamebench service. 
The value is completely ignored if user is not integrated with Gamebench in the cloud service  
Default: false  
Example: false  

## bundleId
Mandatory: Yes (for all iOS runs), No (for any Android runs)  
Description: The reason is the difference in mechanism to install ipa in Bitbar Testing compared to local case. Appium framework maps bundle ID automatically in case of local run/installation. In cloud case we must notify Appium framework about the correct bundle ID.  
Example: desired.bundleId = 'com.bitbar.testdroid.BitbarIOSSample';</pre>  
