# Android-Lock9View [![Download](https://api.bintray.com/packages/takwolf/maven/Android-Lock9View/images/download.svg)](https://bintray.com/takwolf/maven/Android-Lock9View/_latestVersion) [![API](https://img.shields.io/badge/API-5%2B-brightgreen.svg?style=flat)](https://android-arsenal.com/api?level=5) #

An Android grid lock screen view with a callback interface.

## ScreenShot ##

![Screenshot](screenshot/screenshot.png)

## Demo ##

[![Google Play Store](screenshot/git_it_on_google_play.png)](https://play.google.com/store/apps/details?id=com.takwolf.android.lock9)

## Usage ##

### Gradle ###

    compile 'com.takwolf.android:lock9view:0.0.6'

### Layout ###

     

### Explain ###

![Explain](screenshot/explain.png)

 Attention!!! 

If you want to update library reference from version 0.0.4 or earlier,
you should add attributes "lock9_padding" and "lock9_spacing" in your layout to adjust node size(default is 0dp)
otherwise the node size will be changed.

 Attention!!! 

If you want to update library reference from version 0.0.3 or earlier,
you should add a prefix "lock9_" to the Lock9View attributes in your layout, like :

    nodeSrc -> lock9_nodeSrc

This way to solve the resources error if another library has defined the same attributes like :

    "Attribute "xxx" has already been defined"

Thanks for  [@IGZpablocanamares](https://github.com/IGZpablocanamares) .

### Activity ###

    Lock9View lock9View = (Lock9View) findViewById(R.id.lock_9_view);
    lock9View.setCallBack(new CallBack() {

        @Override
        public void onFinish(String password) {
            Toast.makeText(MainActivity.this, password, Toast.LENGTH_SHORT).show();
        }

    });

## What's next ##

Maybe add an error status.

## Author ##

TakWolf

[takwolf@foxmail.com](mailto:takwolf@foxmail.com)

[http://takwolf.com](http://takwolf.com)

## License ##

    Copyright 2015-2016 TakWolf
    
    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)