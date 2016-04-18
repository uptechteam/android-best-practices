# Android best practices

####Tidying Code with Butterknife

Butterknife is simple and lightweight library which allows you to avoid bolierplate code while working with views. Specifically, it allows you to:
 * Eliminate `findViewById` calls by using `@Bind` on fields.
 * Group multiple views in a list or array. Operate on all of them at once with actions,
   setters, or properties.
 * Eliminate anonymous inner-classes for listeners by annotating methods with `@OnClick` and others.
 * Eliminate resource lookups by using resource annotations on fields.


```java
class ExampleActivity extends Activity {
  @Bind(R.id.user) EditText username;
  @Bind(R.id.pass) EditText password;

  @BindString(R.string.login_error)
  String loginErrorMessage;

  @OnClick(R.id.submit) void submit() {
    // TODO call server...
  }

  @Override public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.simple_activity);
    ButterKnife.bind(this);
    // TODO Use fields...
  }
}
```


####Dependency Injection with Dagger 2

Dependency injection is a software design pattern focused on making our applications loosely coupled, extensible, and maintainable.

When you have an object that needs or depends on another object to do its work, you have a dependency. Dependencies can be solved by letting the dependent object create the dependency or asking a factory object to make one. In the context of dependency injection, however, the dependencies are supplied to the class that needs the dependency to avoid the need for the class itself to create them. This way you create software that is loosely coupled and highly maintainable.

Dagger 2 has advantage among other dependency-injection libraries: it implements full-fledged dependency injection framework with generated code. Thus, it's fast (it avoids reflection) and simple to debug.

More info about this dependency injection library can be found on [official Dagger 2 page](http://google.github.io/dagger/users-guide).


####REST Trio: Retrofit, OkHttp, Gson
Retrofit is a type-safe REST client for Android built by Square. The library provides a powerful framework for authenticating and interacting with APIs and sending network requests with OkHttp.

####Make your brain shift with Reactive Programming

####Write shorter code with Retrolambda
[Retrolambda](https://github.com/evant/gradle-retrolambda)** is a Java library for using Lambda expression syntax in Android and other pre-JDK8 platforms. It helps keep your code tight and readable especially if you use a functional style with for example with RxJava.

So things like this:
```java
button.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        log("Clicked");
    }
});
```

Become much simpler:
```java
button.setOnClickListener(v -> log("Clicked"));
```


####Image loading libraries
* Picasso
* Glide
* Fresco


####ORM
* Realm

####Use Stetho to debug your Application
Stetho is a debug bridge for Android applications from Facebook that integrates with the Chrome desktop browser's Developer Tools. With Stetho you can easily inspect your application, most notably the network traffic. It also allows you to easily inspect and edit SQLite databases and the shared preferences in your app. You should, however, make sure that Stetho is only enabled in the debug build and not in the release build variant.

####Build types: debug, staging, release

####Fabric

####Gitignore 
There's a simple way to generate [gitignore file for andorid projects](https://www.gitignore.io/api/linux%2Cwindows%2Cosx%2Candroid%2Cintellij%2Cgradle) on [gitignore.io](www.gitignore.io).

####Recommendations
#####Remember full activity/fragment lifecycle
[Complete Android Fragment & Activity Lifecycle](https://github.com/xxv/android-lifecycle#complete-android-fragment--activity-lifecycle)
#####Beware of the dex method limitation, and avoid using many libraries.
Beware of the dex method limitation, and avoid using many libraries.** Android apps, when packaged as a dex file, have a hard limitation of 65536 referenced methods [[1]](https://medium.com/@rotxed/dex-skys-the-limit-no-65k-methods-is-28e6cb40cf71) [[2]](http://blog.persistent.info/2014/05/per-package-method-counts-for-androids.html) [[3]](http://jakewharton.com/play-services-is-a-monolith/). You will see a fatal error on compilation if you pass the limit. For that reason, use a minimal amount of libraries, and use the [dex-method-counts](https://github.com/mihaip/dex-method-counts) tool to determine which set of libraries can be used in order to stay under the limit. Especially avoid using the Guava library, since it contains over 13k methods.
#####Resource naming conventions
#####Organize packages according to features, not layers

####Thanks To
Jake Wharton, Dima Kovalenko, Andriy Bas
