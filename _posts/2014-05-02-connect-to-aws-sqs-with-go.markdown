---
layout: post
title: "Connect to Aws Sqs with Go"
date: 2014-05-02 13:10:39
categories:
---

Here's a little code snip for connecting to Aws Sqs from Go. It connects to a queue. Posts a message and pops it off and prints it.

It uses the great and very helpful (goamz)[https://github.com/crowdmob/goamz] lib, (sqs package)[https://github.com/crowdmob/goamz/blob/master/sqs/sqs.go].

```go
package main

import (
  "github.com/crowdmob/goamz/sqs"
  "github.com/crowdmob/goamz/aws"
  "fmt"
)

func log_err(err error) {
  if err != nil {
    fmt.Println("Error ---")
    fmt.Println(err)
  }
}

func main() {
  accessKey  := "your key"
  secretKey := "your value"
  queue_name := "golang-test-queue"

  auth := aws.Auth{AccessKey: accessKey, SecretKey: secretKey}
  region := aws.USEast
  aws_sqs := sqs.New(auth, region)

  queue, err := aws_sqs.CreateQueue(queue_name)

  if err != nil {
    fmt.Println(err)
  }

  queue.SendMessage("hello world")

  resp, err := queue.ReceiveMessage(1)

  if err != nil {
    fmt.Println(err)
  }

  fmt.Println("Response ------------")
  fmt.Println(resp)
}
```

Save the above code to a file "sqs-demo.go", compile with `go build` and run it.


--Happy Hacking
