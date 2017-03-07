+++
date = "2015-03-24T22:44:24+05:30"
draft = false
title = "Gorilla mux - Issue with order of routes"
description = "Gorilla mux - Issue with order of routes"
categories = [ "Golang"]
tags = ["golang", "routes"]
author = "Jijesh Mohan"
socialsharing = true
notoc = true
+++

[Gorilla toolkit](gorillatoolkit.org) is one of the favorite http multiplexer library of gophers. I have been using the gorilla mux for quite sometime for micro services.
Mux allows you to define both static and dynamic routes.

Gorilla mux allows you to add similar routes unlike other multiplexer libraries like http-router. Consider the following scenario

```go
router.Handle("/user/{name}",userHandle)
router.Handle("/user/admin",adminHandle)
```

When you hit ``/user/user1`` as expected ```userHandle``` function will be called.
But where as in the case of ```/user/admin``` the ```userHandle``` will be called instead of ```adminHandle```. This means the order of routes matter. Whichever route matches first, will be called by gorilla mux.

One way to fix this issue is to change the order of routes in the above code. This is easy when you have very less number of routes but will become very tedious when the number of routes increases.

There is another way to handle this issue is to sort the routes depends on the length of the path and also ensure that static routes comes before dynamic routes.

Implement [sort](https://golang.org/src/sort/sort.go#12) interface of golang for the endpoints and sort it before adding it to mux router. You can find the implementation  [here](https://github.com/jijeshmohan/janus/blob/master/rest/endpoint.go).
