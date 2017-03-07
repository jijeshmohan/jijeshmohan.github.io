+++
date = "2015-12-27T22:44:24+05:30"
draft = false
title = "Compress http request payload in go"
description = "HTTP request payload compression"
categories = [ "Golang"]
tags = ["golang", "http"]
author = "Jijesh Mohan"
+++

My current project is using golang for the API server. There are multiple type of consumers, including mobile, web and even Smart TV ( in future ) for this API endpoints. One of the API is to send telemetry data from the client which is in json format. Due to the offline feature there are cases where the payload can be huge ( more than 1000 telemetry events in one request). 

We did a calculation on the time it takes to sync 1000 events in one request in various network conditions and the results are: 

{{< figure src="/img/compress-http-result1.png" >}}

To reduce this time, we tried to use couple of binary serialization techniques like Messagepack, protocol buffer etc. But due to the variety of the platforms, we need to support pure JSON format in some cases. So that it leads us to check the normal compression support like any modern web server supports for http response.

This helped us to continue with the same api endpoint with json format itself and with the help of ‘Content-Encoding' header, endpoint determine whether it is a compressed content or not. 

The power of golang [reader](https://golang.org/pkg/io/#Reader) interface can be seen here.

```go

func getData(r *http.Request) (*TelemetryEvents, error) {
	var data TelemetryEvents
	var decoder *json.Decoder
	switch r.Header.Get("Content-Encoding") {
	case "gzip":
		gz, err := gzip.NewReader(r.Body)
		if err != nil {
			return nil, err
		}
		defer gz.Close()
		decoder = json.NewDecoder(gz)
	default:
		decoder = json.NewDecoder(r.Body)
	}
	err := decoder.Decode(&data)
	if err != nil {
		return nil, err
	}
	return &data, nil
}

```

and we have achieved the below numbers without any memory allocation overhead

{{< figure src="/img/compress-http-result2.png" >}}