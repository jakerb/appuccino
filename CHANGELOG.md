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

## `LOAD_ON_CONSTRUCT` Fix
Previously, all elements loaded on construct we're removed once loaded the first time, this has now been fixed to load persistantly when the application construct.

## Trailing-slash in route URI's 
Added `$appuccino.config.router.REMOVE_TRAILING_SLASH` which if set to `true` will rtrim all slashes from route URI's

```javascript
	$appuccino.config.router.REMOVE_TRAILING_SLASH = true;
	// #/home/ = #/home
```

## Debugging flag and Parameters in scope
Added `$scope.app.debugging` and `$scope.app.parameters` to the scope app object to stop code repeats and unnecessary variable setting in app hooks.

## Added hook `application/view/rendered`
This hook will fire when the DOM has completely loaded, this has been added so that heavy data manipulation which would cause the DOM to break rendering can be done after load.

## Added hook `application/controller/post/{post_name}`
To be used where a specific post name is active.

## Added hook `application/controller/post/id/{id}`
To be used where a specific post ID is active.

## Added hook `application/controller/template/{template}`
To be used where a specific template is active. (Where template path would be `templates/demo.html` the hook would remove the extension)

```javascript
$appuccino.action.do('application/controller/template/templates/demo', function() {
	console.info('I am running on views using the templates/demo.html template');
});
```

##