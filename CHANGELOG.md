# 2.0.0
## Major release jump!
iOS 13 deprecation of UIWebView means that WKWebView has now been implemented throughout the Appuccino platform as well as an entirely new engine for both iOS and Android. 

This latest release offers greater control of application code as well as smoother transitions, background processing and error handling.

## Configurator
Rather than having to manually set configuration within your controllers you can now make use of the `application/config` hook to set runtime configuration.

```javascript
// Add a new action hook for application/config, this will expose the config setter as $this.

$appuccino.action.add('application/config', function() {

	this.set({
		ptr: false //Disable PullToRefresh
		swipe: false //Disable Edge Swipe
		config: {
			router: {
				//Modify existing configuration
				PROMPT_FETCH_RELOAD: false ,

				//Add your own custom variables
				CUSTOM_VAR: 'Hello World'
			}
		}
	});

});

```

### Smoother Transitions
The core page transitions have been updated to change on construct of the controller, this reduces in-between view flash and waits for any heavy computation to complete before transitioning to the next view.

### Runtime File Checking
In previous versions of appuccino, if a file had changed, the view would load the old version and download the new version in the background, this required the user either refreshing or reloading the app to get the latest changes.

In this version we have set all file changes to download and render only the latest version so you don't need to relaunch to get the latest changes.

We have also added a hook to fetch changes whilst the app is running - this will check for any changes to the manifest and reload the app with the updates.

```javascript
// Use fetch to look for app changes.
$appuccino.action.do('capacitor/application/fetch');
```

By default, a snackbar notification will appear with the message `A new version of this app is available. Update now?`this prompt can be disabled and will simply reload the app by setting `PROMPT_FETCH_RELOAD` config variable to `false`.



# 1.2.0

## Toggle splash-screen text and loading bar
Using the new splash plugin in the app scope `$scope.splash` it is now easy to hide and show elements (app reload/restart required).

```javascript
// Hide the loader bar
$scope.splash.hide_progress();

// Hide the loader label
$scope.splash.hide_label();

// Hide both at once
$scope.splash.hide();

// Show the loader bar
$scope.splash.show_progress();

// Show the loader label
$scope.splash.show_label();

// Show both at once
$scope.splash.show();
```

## Load on Construct Fix
Previously, all elements loaded on construct we're removed once loaded the first time, this has now been fixed to load persistantly when the application construct.

## Trailing-slash in route URI's 
Added `$appuccino.config.router.REMOVE_TRAILING_SLASH` which if set to `true` will rtrim all slashes from route URI's

```javascript
	$appuccino.config.router.REMOVE_TRAILING_SLASH = true;
	// #/home/ = #/home
```

## Debugging flag and Parameters in scope
Added `$scope.app.debugging` and `$scope.app.parameters` to the scope app object to stop code repeats and unnecessary variable setting in app hooks.

## Added hook application/view/rendered
This hook will fire when the DOM has completely loaded, this has been added so that heavy data manipulation which would cause the DOM to break rendering can be done after load.

## Added hook application/controller/post/{post_name}
To be used where a specific post name is active.

## Added hook application/controller/post/id/{id}
To be used where a specific post ID is active.

## Added hook application/controller/template/{template}
To be used where a specific template is active. (Where template path would be `templates/demo.html` the hook would remove the extension)

```javascript
$appuccino.action.do('application/controller/template/templates/demo', function() {
	console.info('I am running on views using the templates/demo.html template');
});
```

## Try and Catch on application/controller/construct
Added to improve debugging on the controller.

## Reset View Y Position
Added `$app.config.router.RESET_SCROLL_POSITION` which if set to true resets the page Y position to `0` on view change.

## iOS Transition Delay
Added `$app.config.router.IOS_DELAY` for transition iOS delay.

## Background Jobs
Added background plugin (accessible via `$appuccino.application.background`) which creates promise jobs to stop render blocking computation.

## Store Files Locally
Added cache plugin (accessible via `$scope.cache`) to store files into local storage from a URL.

```javascript
$scope.cache.file('https://github.com/jakerb/appuccino/raw/master/src/img/appuccino-logo.png').then(function(path) {
	if(typeof path == 'string') {
		$scope.logo = path;
	}
});

```

## Other Fixes
- Fix to components plugin priority
- Update to the UI for PTR (PullToRefresh)
- Added CordovaPromiseFS and CordovaFileCache
- Added Socket IO
- Fix to `.map` console errors in web-animations and other stylesheets