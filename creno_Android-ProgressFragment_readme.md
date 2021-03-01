Android-ProgressFragment
========================

[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-Android--ProgressFragment-brightgreen.svg?style=flat)](https://android-arsenal.com/details/1/366)

Implementation of the fragment with the ability to display indeterminate progress indicator when you are waiting for the initial data. Based on [ListFragment](http://developer.android.com/reference/android/app/ListFragment.html).


Sample
------

A sample application is available on Google Play:

 
   
 

![screenshot][1]


Compatibility
-------------

This library is compatible from API 4 (Android 1.6).


Usage
-----

To display the progress fragment you need the following code:

* Create your implementation of progress fragment

``` java
public class MyProgressFragment extends ProgressFragment {
	// your code of fragment
}
```

or if you use [ActionBarSherlock](https://github.com/JakeWharton/ActionBarSherlock)

``` java
public class MyProgressFragment extends SherlockProgressFragment {
	// your code of fragment
}
```

* Setup content view and empty text (optional) in `onActivityCreate()` method.

``` java
@Override
public void onActivityCreated(Bundle savedInstanceState) {
    super.onActivityCreated(savedInstanceState);
    // Setup content view
    setContentView(R.layout.content);
    // Setup text for empty content
    setEmptyText(R.string.empty);
    // ...
}
```

* Display of indeterminate progress indicator

``` java
setContentShown(false);
```


* When the data is loaded to set whether the content is empty and show content

``` java
setContentEmpty(/* true if content is empty else false */);
setContentShown(true);
```


Gradle
------

Android-ProgressFragment library is now pushed to Maven Central as a AAR, so you just need to add the following dependency to your build.gradle.

ProgressFragment (support-v4):
``` xml
dependencies {
    compile 'com.github.johnkil.android-progressfragment:progressfragment:1.4.+'
}
```

ProgressFragment (native):
``` xml
dependencies {
    compile 'com.github.johnkil.android-progressfragment:progressfragment-native:1.4.+'
}
```

SherlockProgressFragment:
``` xml
dependencies {
    compile 'com.android.support:support-v4:19.0.0'
    compile('com.github.johnkil.android-progressfragment:sherlockprogressfragment:1.4.+') {
        exclude module: 'support-v4'
    }
}
```

Example Gradle project using Android-ProgressFragment:

* [Android-ProgressFragment-Gradle-Sample](https://github.com/johnkil/Android-ProgressFragment-Gradle-Sample)


Developed By
------------
* Evgeny Shishkin -  


License
-------

    Copyright 2013 Evgeny Shishkin
    
    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at
    
    http://www.apache.org/licenses/LICENSE-2.0
    
    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
    
[1]: http://i44.tinypic.com/34ffncx.png

[0]: https://github.com/jkwiecien/Switcher


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)