---
title: o[andrioid] Xamarin - Application Hello World - Package Size
author: PipisCrew
date: 2016-03-11
categories: [android]
toc: true
---

source - [https://developer.xamarin.com/guides/android/advanced_topics/application_package_sizes/](https://developer.xamarin.com/guides/android/advanced_topics/application_package_sizes/)

In order to ship a fully contained application, the package must include the application, the associated libraries, the content, the Mono runtime, and the required Base Class Library (BCL) assemblies. For example, if we take the default "Hello World” template, the contents of a complete package build would look like this: 15mb

15.8 MB is a larger download size than we’d like. The problem is the BCL libraries, as they include mscorlib, System, and Mono.Android, which provide a lot of the necessary components to run your application. However, they also provide functionality that you may not be using in your application, so it may be preferable to exclude these components.

When we build an application for distribution, we execute a process, known as Linking, that examines the application and removes any code that is not directly used. After running the linker on the Hello World application, our package now looks like this: 2.9mb

android linker - [https://developer.xamarin.com/guides/android/advanced_topics/linking/](https://developer.xamarin.com/guides/android/advanced_topics/linking/)
ios linker - [https://developer.xamarin.com/guides/ios/advanced_topics/linker/](https://developer.xamarin.com/guides/ios/advanced_topics/linker/)
ios download file (sample) - [https://developer.xamarin.com/recipes/ios/network/web_requests/download_a_file/](https://developer.xamarin.com/recipes/ios/network/web_requests/download_a_file/)

## samples

[https://github.com/xamarin/xamarin-forms-samples](https://github.com/xamarin/xamarin-forms-samples)

# Push Notification

[https://github.com/rdelrosario/xamarin-plugins/tree/master/PushNotification](https://github.com/rdelrosario/xamarin-plugins/tree/master/PushNotification)

origin - http://www.pipiscrew.com/?p=4335 andrioid-xamarin-application-hello-world-package-size