---
layout: post
title: "Dequeue SQS Messages into a Directory"
date: 2014-05-05 08:31:16
categories:
---

Here's a little snip that can be helpful when working with SQS. It allows you to dequeue messages and write them to a directory so you can experiment or run tests locally.

```ruby
#!/usr/bin/env ruby

require 'aws-sdk'
require 'trollop'
require 'ostruct'

options = Trollop::options do
  banner <<-EOS
Download messages from an AWS SQS queue and write then to a directory.

Usage: #{$0} [options] <queuename>
options:
EOS
  opt :dir, "Directory to write messages to. Defaults to queue name", type: :string, default: ARGV.first
  opt :timeout, "Max timeout in secs", default: 3
  opt :max_messages, "Max number of messages to fetch", default: 1000
  opt :quiet, "Silence output", default: false
end
Trollop::die "No queue given" if ARGV.size == 0

sqs = AWS::SQS.new
queue = sqs.queues.create ARGV.first
msg_cnt = 0
Dir.mkdir opts.dir unless Dir.exist? opts.dir

puts "Dequeueing #{opts.max_messages} from #{ARGV.first}" unless opts.quiet
queue.poll idle_timeout: opts.idle_timeout, wait_time_seconds: opts.timeout do |msg|
  break unless msg
  fname = [Time.new.strftime("%Y%m%d-%H%M%S-%L"), ARGV.first, msg.id, msg.md5].join('.')
  fpath = File.join opts.dir, fname
  File.open(fpath, 'w') { |f| f.write msg.body }
  puts fpath unless opts.quiet
  break if (msg_cnt += 1) == opts.max_messages
end
```
