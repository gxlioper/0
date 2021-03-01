# AndroidKeyboardWatcher
Software keyboard open/close watcher for Android.

Android SDK doesn't provide direct way to track open/close events from software keyboard. This small library does it for you.

![AndroidKeyboardWatcher](https://raw.githubusercontent.com/AzimoLabs/AndroidKeyboardWatcher/master/art/keyboard_shown.png)

## Usage

Make sure that you use `adjustResize` windowSoftInputMode in your Acitivty configuration in AndroidManifest.xml:

```xml
 
```

Bind KeyboardWatcher in your `Activity.onCreate()` method. To prevent memory leaks make sure to unbind it in `onDestroy()` method.

```java
public class MainActivity extends Activity implements KeyboardWatcher.OnKeyboardToggleListener {
    private KeyboardWatcher keyboardWatcher;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        //...
        keyboardWatcher = new KeyboardWatcher(this);
        keyboardWatcher.setListener(this);
    }

    @Override
    protected void onDestroy() {
        keyboardWatcher.destroy();
        super.onDestroy();
    }

    @Override
    public void onKeyboardShown(int keyboardSize) {
        
    }

    @Override
    public void onKeyboardClosed() {
        
    }
}
```

## Download

### Java code

If you don't want to add another dependency to your project, just copy [KeyboardWatcher.java](https://github.com/AzimoLabs/AndroidKeyboardWatcher/blob/master/keyboardwatcher/src/main/java/com/azimolabs/keyboardwatcher/KeyboardWatcher.java) to your source directory.

### Library dependency

```gradle
dependencies {
  compile 'com.azimolabs.keyboardwatcher:keyboardwatcher:0.1.3'
}
```


## License

    Copyright (C) 2016 Azimo

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