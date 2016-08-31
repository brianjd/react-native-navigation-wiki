Migrating your code base to version 2.0 will require a few changes to your native Java code. The actual navigation API has not changed so there will be no changes to your JS code base.

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
* Implement `isDebug` and `createAdditionalReactPackages`

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
