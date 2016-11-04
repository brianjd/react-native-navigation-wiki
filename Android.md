# Activity Lifecycle and onActivityResult
In order to listen to activity lifecycle callbacks, set `ActivityCallback` in `MainApplication.onCreate` as follows:

```java
public class MainApplication extends NavigationApplication {
    @Override
    public void onCreate() {
        super.onCreate();
        setActivityCallbacks(new ActivityCallbacks() {
            @Override
            public void onActivityCreated(Activity activity, Bundle savedInstanceState) {
                
            }

            @Override
            public void onActivityStarted(Activity activity) {
                
            }

            @Override
            public void onActivityResumed(Activity activity) {
                
            }

            @Override
            public void onActivityPaused(Activity activity) {
                
            }

            @Override
            public void onActivityStopped(Activity activity) {
                
            }

            @Override
            public void onActivityResult(int requestCode, int resultCode, Intent data) {
                
            }

            @Override
            public void onActivityDestroyed(Activity activity) {
                
            }
        });
    }
}
```

## Why overriding these methods in `MainActivity` won't work
`MainActivity` extends `SplashActiviy` which is used to start the react context. Once react is up and running `MainActivity` is **stopped** and another activity takes over to run our app: `NavigationActivity`. Due to this design, there's usually no point in overriding lifecycle callbacks in `MainActivity`.

# Splash screen
Override `getSplashLayout` or `createSplashLayout` in `MainActivity` to provide a splash layout which will be displayed while Js context initialises.
