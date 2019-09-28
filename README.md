# najva Ionic Application
This is a `Ionic` application that `Najva_cordova_plugin` implemented in it.

### Test Najva Service in Ionic
If you want test `Najva Push Notification Service` in `ionic` application you should:

1.  Clone this project and rename package name of it 

2.  Register this app after login in [najva panel](https://app.najva.com/accounts/login/?next=/).(to register any app, its package name must be unique!)


3.  After register najva panel gives you `websiteId`,`apiKey` which is specific to your app

4.  Go to `config.xml` file and put this parameters looks like the following then save it.
```
<widget xmlns:android="http://schemas.android.com/apk/res/android">

    <platform name="android">

        <config-file target="AndroidManifest.xml" parent="/manifest/application">
             <meta-data
                android:name="com.najva.sdk.metadata.API_KEY"
                android:value="[YOUR_API_KEY_GOES_HERE]" />
            <meta-data
                android:name="com.najva.sdk.metadata.WEBSITE_ID"
                android:value="[YOUR_WEBSITE_ID_GOES_HERE]" />
        </config-file>

    </platform>

</widget>
```
put `websiteId` and `apiKey` here!

then go to `src/index.html` and add the following script to body of it.
```
<script type="text/javascript">
    document.addEventListener("deviceready", deviceReady, true);
    function deviceReady() {
        window.najva.init(function(success){
        console.log("najav_init successful");
        },function(error){
        console.log("najav_init fail");
        });
        window.najva.receiveJSONNotifications(function (json) {
            console.log("reveiveJSON: " + json);
            //todo handle json here
        });
        window.najva.handleUsers(function (token) {
                //todo send token to your server.
                console.log("token: " + token);
        });

    }
</script>
```

5.  Now you can run application and send notification from your panel to it!



