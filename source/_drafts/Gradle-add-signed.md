---
title: Android 通过 Gradle 自动添加证书签名
date: 2015-09-19 09:55:35
---

在需要打包项目根目录新建`filename.properties`文件

`signed.properties`
```ruby

KEYSTORE_FILE = 用于签名多证书所在目录
KEYSTORE_PASSWORD = 证书密码
KEY_ALIAS = 证书的别名
KEY_PASSWORD = 别名的密码
```

`build.gradle`

```ruby
Properties props = new Properties()
props.load(new FileInputStream(file("signed.properties")))

android {
  signingConfigs {
    release {
      keyAlias props['KEY_ALIAS']
      keyPassword props['KEY_PASSWORD']
      storeFile file(props['KEYSTORE_FILE'])
      storePassword props['KEYSTORE_PASSWORD']
    }
  }

  buildTypes {
    release {
      signingConfig signingConfigs.release
    }
    debug {
      signingConfig signingConfigs.release
    }
  }
}
```
