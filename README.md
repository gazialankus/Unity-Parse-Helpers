Unity-Thenable-Tasks
===================

This library is based on [Unity-Parse-Helpers][1]. 

Since Firebase uses [Parse's Unity Tasks library](https://github.com/parse-community/Parse-SDK-dotNET/tree/master/Unity.Tasks), I found [Unity-Parse-Helpers][1] to be useful. However, it also has other Parse-related things that we don't need in Firebase and that prevent compilation without Parse. So, I created this repo to host only the task-related parts of [Unity-Parse-Helpers][1]. 

Below are the related documentation from [Unity-Parse-Helpers][1]. 

This library provides a number of helpers and utilities for dealing with Parse.com in Unity 3D

Task Chaining
--------------

A series of extension methods have been provided that let you chain together calls in a Javascript-Promise like manner:

```
 // Signup
userService.Signup(usernameInp.text, passwordInp.text, playernameInp.text)

	// Then Login
	.Then(t => userService.Login(usernameInp.text, passwordInp.text))

	// Then we are done
	.Then(OnLoggedIn, OnError);             
```

Looming
-------

Using the extension ".OnMainThread()" for Task you can ensure that your Parse async calls always run in the main thread:

```
public Task<GameUser> Login(string email, string password)
{
	Debug.Log("Logging in..");

	return ParseUser.LogInAsync(email, password)
		.OnMainThread()
		.Then(t => Task.FromResult((GameUser)t.Result));
}
```

Installation
------------

Checkout this project as a sub-module in your project, and you should be good to go!


[1]: https://github.com/mikecann/Unity-Parse-Helpers