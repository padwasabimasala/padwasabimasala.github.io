---
layout: post
title: "Getting Going with Go"
date: 2014-05-02 13:32:08
categories:
---

Coming from Ruby (Go for a Rubyist)[http://supermar.in/go-for-a-rubyist/] is a awesome and easy to follow introduction to go.

If you're interested in running web apps in heroku you should take a look at (Mark McGranaghan's updated article)[http://mmcgrana.github.io/2012/09/getting-started-with-go-on-heroku.html] on the subject. I ran into a little trouble installing (godep)[http://github.com/kr/godep] on MacOSX though, because it depends on mercurial. The fix was to use brew to uninstall and reinstall python, and mercurial, and then do this hack.

```
cd ~/
mkdir .MacOSX
cat > .MacOSX/environment.plist <<EOS
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
  <key>Prefer-32-Bit</key>
  <true/>
</dict>
</plist>
EOS
```
