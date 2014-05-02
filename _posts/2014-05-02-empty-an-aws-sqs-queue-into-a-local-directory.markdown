---
layout: post
title: "Empty an Aws Sqs Queue into a Local Directory"
date: 2014-05-02 16:32:26
categories:
---

This little script will empty an AWS SQS queue into a local directory. 

```ruby
#!/usr/bin/env ruby
require 'aws-sdk'
require 'trollop'
require 'ostruct'

options = Trollop::options do
  opt :dir, "Directory to write messages to", default: "./#{ARGV.first}"
  opt :idle_timeout, "Max idle time in secs", default: 1
  opt :max_messages, "Max number of messages to fetch", default: 1000
end

opts = OpenStruct.new options
sqs = AWS::SQS.new
queue = sqs.queues.create ARGV.first
msg_cnt = 0
Dir.mkdir opts.dir unless Dir.exist? opts.dir

queue.poll idle_timeout: opts.idle_timeout do |msg|
  break unless msg
  puts msg.id
  fname = File.join opts.dir, msg.id
  File.open(fname, 'w') { |f| f.write msg.body }
  msg_cnt += 1
  break if msg_cnt == opts.max_messages
end
```
