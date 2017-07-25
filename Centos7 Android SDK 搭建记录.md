登录远程机器
----------------------
`ssh root@192.168.100.43`

下载
----------------------
```
 wget https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip 

 mkdir /usr/lib/android-sdk 

 unzip -o sdk-tools-linux-3859397.zip -d /usr/lib/android-sdk 


```

配置 AndroidSDK 环境
----------------------

> vi /etc/profile.d/android-sdk-env.sh
> 
```
export ANDROID_HOME="/usr/lib/android-sdk"
export PATH="$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools:$ANDROID_HOME/tools/bin:$PATH"

```

> source /etc/profile.d/android-sdk-env.sh

下载SDK内的包
----------------------
```
//查看列表
sdkmanager --list

//更新需要的包
sdkmanager "platform-tools" "platforms;android-26" "platforms;android-19" "platforms;android-24" "platforms;android-25" "platforms;android-14" "build-tools;26.0.0" "build-tools;25.0.1" "extras;google;m2repository" "extras;google;webdriver" "extras;google;play_billing" "extras;android;m2repository" "extras;android;gapid;3"

```

遇到的问题
----------------------
> Warning: File /root/.android/repositories.cfg could not be loaded.
> 
> 解决方案：
> touch /root/.android/repositories.cfg

