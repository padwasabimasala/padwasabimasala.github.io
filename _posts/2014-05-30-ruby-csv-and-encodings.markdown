---
layout: post
title: "Ruby CSV and Encodings"
date: 2014-05-30 08:48:19
categories:
---

I kept getting encoding errors while trying to parse a CSV *string* in Ruby.

```
 ArgumentError: invalid byte sequence in UTF-8
```

After googling I found a possible solution at http://blog.andreamostosi.name/2013/06/encoding-csv-and-ruby/

So I tried passing the encoding to `CSV.parse` but got the same error.

```ruby
  contents = CSV.parse(csv_string, encoding: "iso-8859-1")
```

The post also suggests forcing the coding of the string like so

```ruby
  contents.encode!("iso-8859-1", "utf-8", :invalid => :replace)
```

This elimniated the error but caused some characters to not be correctly transcoded.

Not replacing invalid characters raised a new error

```ruby
  contents.encode!("iso-8859-1", "utf-8")
```

Results in

```
  "\xE7" followed by "u" on UTF-8 (Encoding::InvalidByteSequenceError)
```

I was skeptical about what the encoding actually was so I googled about and came across http://www.rodrigoalvesvieira.com/ruby-to-find-out-file-encoding/

Which suggested that I try `String#encoding`

```ruby
   puts contents.encoding
   => 'UTF-8'
```

That didn't seem right so I ended up using [Charlock Holmes](https://github.com/brianmario/charlock_holmes)

It depends on the ICU library which can be install with brew on OSX `brew install icu4u`

Eventually I came to http://stackoverflow.com/questions/7047944/ruby-read-csv-file-as-utf-8-and-or-convert-ascii-8bit-encoding-to-utf-8 which led to my final solution.

```ruby
require 'charlock_holmes'
require 'csv'

contents = File.read 'file.csv'

meta = CharlockHolmes::EncodingDetector.detect contents
encoding = meta[:encoding]
utf8_contents = contents.force_encoding(encoding).encode('utf-8')

CSV.parse(utf8_contents).each do |row|
  p row
end
```

Happy Hacking
--PWM
