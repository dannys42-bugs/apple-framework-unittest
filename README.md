# apple-framework-unittest
Demonstrates a possible bug in unit testing frameworks on-device

# Steps to Reproduce

1. Create Framework project called 'SomeFramework' with Unit-Tests
2. Create 'TestHostApp' (a single UIView app with no additional logic)
3. Set Host Application for to 'SomeFramworkTests' to 'TestHostApp'
4. Run unit-tests in Simulator (success)
5. Run unit-tests on Device (failure)

# Failures

There are two failures:

1. Step #5 above failes on Device.  Go to Build logs and see the following error:

```
TestHostApp.app (24168) encountered an error (Failed to load the test bundle. (Underlying error: The bundle “SomeFrameworkTests” couldn’t be loaded because it is damaged or missing necessary resources. The bundle is damaged or missing necessary resources. dlopen_preflight(/var/containers/Bundle/Application/C39ED8FD-58E0-491F-92AF-F89463B2B496/TestHostApp.app/PlugIns/SomeFrameworkTests.xctest/SomeFrameworkTests): Library not loaded: @rpath/SomeFramework.framework/SomeFramework
  Referenced from: /var/containers/Bundle/Application/C39ED8FD-58E0-491F-92AF-F89463B2B496/TestHostApp.app/PlugIns/SomeFrameworkTests.xctest/SomeFrameworkTests
  Reason: image not found))
```

2. If Step #5 is done after a successful run on simulator, the test status in the navigator still appears as success, even though the tests were unable to execute due to the above failure.  If you do not go to the Build logs you may miss this error.


# Test Environment

- MacOS 10.15.6
- iOS 13.7 on iPhone 11 Pro
- Xcode 11.7 and 12.0.1
