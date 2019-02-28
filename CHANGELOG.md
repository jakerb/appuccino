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