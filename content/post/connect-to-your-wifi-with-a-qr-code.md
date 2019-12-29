+++
author = "Frank Adrian"
comments = true
cover = "/uploads/IMG_B15F4C34246A-1.jpeg"
date = 2019-12-28T23:00:00Z
tags = ["macos", "ios", "android"]
title = "Connect to your WiFi with a QR code"

+++
# Connect to your WiFi with a QR code

It's possible to generate a QR code that you can use to connect to the WiFi without having to manually enter the password. To do this you can use this [open-source](https://github.com/evgeni/qifi "https://github.com/evgeni/qifi") [website](https://qifi.org/ "https://qifi.org/"), or preferably, you can use the `qrencode` cli tool.

To install [qrencode](https://packages.debian.org/stable/qrencode "https://packages.debian.org/stable/qrencode") on MacOS you can use homebrew.

    brew install qrencode

Then to generate the QR code

    qrencode -o wifi.png "WIFI:T:WPA;S:<SSID>;P:<PASSWORD>;;"

Replace <SSID> with your Network Name and <PASSWORD> with your password and you are good to go.

Credits:

[https://feeding.cloud.geek.nz/posts/encoding-wifi-access-point-passwords-qr-code/](https://feeding.cloud.geek.nz/posts/encoding-wifi-access-point-passwords-qr-code/ "https://feeding.cloud.geek.nz/posts/encoding-wifi-access-point-passwords-qr-code/")