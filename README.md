# 准备工作

## 搜索插件 : Flutter Intl

![插件](http://pictures-upyun.test.upcdn.net/img/20200413204441591.png)

## 项目配置

添加依赖:

```
dev_dependencies:
...
  //add this
  flutter_localizations:
    sdk: flutter

```

在菜单栏的Tool下找到Flutter Intl 并选择Initalize for the project， 配置结束后效果如下：

![image-20200819233727693](http://pictures-upyun.test.upcdn.net/img/image-20200819233727693.png)

1. **会在 pubspec.yaml中增加以下字段**

```
flutter_intl:  
    enabled: true
```

2. **会在lib目录下增加 generated 和 l10n两个包**

![image-20200819234311852](http://pictures-upyun.test.upcdn.net/img/image-20200819234311852.png)

- generated包下的intl包默认存在一个**messages_all.dart**和**messages_en.dart**文件，messages开头的文件会在添加语言后自动生成
- l10n包下存在一个intl_en.arb文件

3. **使用`Add Locale`生成其他语言的arb文件**

   ![image-20200819234431082](http://pictures-upyun.test.upcdn.net/img/image-20200819234431082.png)

例如:zh_CN , 会在l10n包下生成Intl_zh_CN.arb文件 , 可在其中填入对应的文案.

4. **设置国际化语言**

```dart
return MaterialApp(
  ...
    localizationsDelegates: const [
      S.delegate,
      GlobalMaterialLocalizations.delegate,
      GlobalCupertinoLocalizations.delegate,
      GlobalWidgetsLocalizations.delegate
    ],
    supportedLocales: S.delegate.supportedLocales,
    localeListResolutionCallback: (locales, supportedLocales) {
      print(locales);
      return;
    },
  ...
);

```

5. 使用

在需要配置国际化的地方调用`S.of(context).key`即可.

没有`context` 时可以使用`S.current.key`



*注意 :*

1. 支持语言的顺序为字符串排序 (如zh_A会在zh_B之前) , 并非添加语言的顺序.
2. 假设系统语言为`zh_TW` , 项目并不支持,会优先寻找`zh`的其他语言 , 以`supportedLocales`顺序从上向下寻找.
3. 旧版本i18n插件生成的为`i18n`文件夹 , 而`flutter intl`生成的为`l10n` , 首字母不同 , 需要注意.
4. 此方式无需依赖`intl`包 , 但不提供`intl`相关功能. 需要额外功能才需要依赖`intl`.
5. 如不想弃用旧版intl的AS插件,但AS版本又不支持,可使用该插件生成的dart代码替代`i18n`中的代码,但可能需要修改类名.


