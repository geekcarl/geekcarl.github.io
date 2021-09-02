# Android 自动加固打包插件

## 优势
* 1, 支持多变体，可自定义多个buildType配置
* 2，支持多风味，可自定义多个productFlavor
* 3，支持美团walle多渠道配置（提升打包效率），采用walle-cli-all.jar工具
* 4，支持自定义输出apk文件名, 完全兼容variant.output.outputFileName 自定义文件名方式，加固打包会在已配置文件名上追加部分信息。
* 5，支持加固签名后生成git提交信息到文件名上，方便追踪版本记录
  

## 怎么用
### 1，添加配置文件[reinforce.properties](reinforce.properties) 到项目根目录
```properties
# 所有配置路径的参数都是相对${project.rootDir}的路径

# 360加固jar包配置，必须
reinforce.jar=reinforce/jiagu/jiagu.jar
# 更换为自己的360开发者账号，必须
reinforce.account="sinoagri"
# 360开发者账号密码，必须
reinforce.password="Sinoagri8848"
# 加固输出路径，（选配，默认为${project.buildDir}/outputs/reinforce）
reinforce.outputPath=reinforceOutput

# 签名配置（选配，默认读取android.buildTypes.$buildType.signingConfig配置）
sign.storeFile=app/reinforce.jks
sign.storePassword=123456789
sign.keyAlias=reinforcedemo
sign.keyPassword=123456789

# V2签名校验工具 (选配，如果不配置就不会校验，最好还是配置下)
sign.checkV2Jar=reinforce/sign/checkAndroidV2Signature.jar

# 美团多渠道打包（选配)
walle.enable=true
# 美团walle cli工具
walle.jar=reinforce/walle/walle-cli-all.jar
# 美团channel配置文件
walle.channel=channel
```

### 2，在app/build.gradle中添加gradle远程插件依赖
```gradle

apply from: 'https://geekcarl.github.io/gradle-reinforce/reinforce.gradle'

```

### 3，打包
* 1，在项目根目录执行： `./gradlew tasks ` 
* 2，会发现task group为 `reinforce` task list
* 3, 执行你的目标`task`吧


