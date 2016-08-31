* Make sure you are using react-native version 0.25.1

 >Note: Android adaptation is still under active development therfore the API might break from time to time. 
 
1.  Add the following to your `settings.gradle` file located in the `android` folder:

	```groovy
	include ':react-native-navigation'
	project(':react-native-navigation').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-navigation/android/app/')
	```
	
2. Update project dependencies in `build.gradle` under `app` folder.

	```groovy
	dependencies {
	    compile fileTree(dir: "libs", include: ["*.jar"])
	    compile "com.android.support:appcompat-v7:23.0.1"
	    compile "com.facebook.react:react-native:+"
	    debugCompile project(path: ':react-native-navigation', configuration: 'libraryDebug')
	    releaseCompile project(path: ':react-native-navigation', configuration: 'libraryRelease')
}
```

3. Your `MainActivity` should extend `com.reactnativenavigation.controllers.SplashActivity` instead of `ReactActivity`. If you have any `react-native` related methods in your `MainActivity` you can safely delete them.

4. Create a custom Application class and update the `Application` element in `AndroidManifest.xml`
	
	```java
	import com.reactnativenavigation.NavigationApplication;
	
	public class MyApplication extends NavigationApplication {
	
	}
	```
	
	```xml
	<application
        android:name=".MyApplication"
        ...
        />
	```
5. Implement `isDebug` and `createAdditionalReactPackages` methods

	```java
	import com.reactnativenavigation.NavigationApplication;
	
	public class MyApplication extends NavigationApplication {
 
    	@Override
		public boolean isDebug() {
			// Make sure you are using BuildConfig from your own application
			return BuildConfig.DEBUG;
		}

	    @NonNull
	    @Override
	    public List<ReactPackage> createAdditionalReactPackages() {
		    // Add the packages you require here.
			// No need to add RnnPackage and MainReactPackage
	        return null;
	    }
	}
	```