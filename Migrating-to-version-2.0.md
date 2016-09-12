Migrating your code base to version 2.0 will require a few changes to your native Java code. 

If you updated your project to `react-native` version > 30 you probably did most of those changes (like creating an `Application` class, in any case, if you have any questions please review https://facebook.github.io/react-native/docs/upgrading.html before opening an issue.

Currently, the actual navigation API has not changed so there will be no changes to your JS code base.

* In your `build.gradle` change your `dependencies` to point to `compile project(':react-native-navigation')`
* Your `MainActivity` should now extend `com.reactnativenavigation.controllers.SplashActivity`
* Delete the `getPackages()` from `MainActivity`. Don't forget to delete unused imports after this step.
* Create a custom Application class and update the `Application` element in `AndroidManifest.xml`
	
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
* Implement `isDebug` and `createAdditionalReactPackages` in your `MyApplication` class

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
