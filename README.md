# 发布 android library 到 jcenter
**本仓库包含了关于通过 bintray.com 将 android library 上传到 jcenter 的文件。** 
> 因为在 AndroidStudio 中通过 [bintray-release](https://github.com/novoda/bintray-release) 的方式发布遇到了很多坑（头坑是 Gradle 版本不兼容），所以采用原始的方法。

## 第 0 步
> 注册好 [bintray](https://bintray.com) 的账号，并得到 apikey。
## 第 1 步
> 在 bintray 中创建好一个放 library 仓库。例如 'just'，类型要选 **maven**。
## 第 2 步
> 在 project 的 build.gradle 引入插件。
```gradle
classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.8.4' // 用于上传
classpath 'com.github.dcendents:android-maven-gradle-plugin:2.1' // 用于打包
```
## 第 3 步
> 在 project 的 local.properties 中配置 bintray.user 和 bintray.apikey。
## 第 4 步
> 在要上传的 library 的 build.gradle 中配置 pom 和 bintray 信息，位置与 dependencies **同级别**。
以 [just-mvp](https://raw.githubusercontent.com/groooooomit/just-mvp/master/JustMvp/just-mvp/build.gradle) 为例
```gradle
ext {
    gitUrl = 'https://github.com/groooooomit/just-mvp.git'
    siteUrl = 'https://github.com/groooooomit/just-mvp'

    // pom 配置
    pom_groupId = 'com.bfu'
    pom_artifactId = 'just-mvp'
    pom_version = '1.0.0'
    pom_name = 'just-mvp'
    pom_description = 'A mvp library for android.'
    pom_licenseName = 'The Apache Software License, Version 2.0'
    pom_licenseUrl = 'http://www.apache.org/licenses/LICENSE-2.0.txt'
    pom_developerId = 'groooooomit'
    pom_developerName = 'groooooomit'
    pom_developerEmail = 'fubofubo@hotmail.com'

    // bintray package 配置
    bintray_repo = 'just' // 这里的仓库名对应 bintray 中的 maven 仓库
    bintray_name = 'mvp' // 这将会在仓库 'just' 中生成一个名为 'mvp' 的 package
    bintray_desc = '> A mvp library for android.'
    bintray_licenses = ["Apache-2.0"]
}
```
## 第 5 步
> 在 library 的 build.gradle **末尾**引入用于打包和上传的 gradle 脚本。
```gradle
apply from: 'https://raw.githubusercontent.com/groooooomit/jcenter/master/jcenter-maven-install.gradle'
apply from: 'https://raw.githubusercontent.com/groooooomit/jcenter/master/jcenter-bintray-config.gradle'
```
## 第 6 步
> 打开 AndroidStudio 的 Terminal，执行发布命令。输出 BUILD SUCCESSFUL ... 表明上传成功。
```gradle
gradlew clean build install bintrayUpload
```
## 第 7 步
> 将上传的 library 提交到 jcenter 审核。
> 按钮的位置在 home -> repositories -> just -> mvp -> Actions -> Add to jcenter
# 致谢
[How to publish Android Library on Bintray/JCenter](http://blogs.quovantis.com/how-to-publish-android-library-on-bintrayjcenter/)
