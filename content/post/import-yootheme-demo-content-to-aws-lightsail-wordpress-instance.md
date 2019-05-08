+++
author = "Frank Adrian"
comments = false
cover = ""
date = ""
draft = true
tags = []
title = "Import Yootheme demo content to aws lightsail wordpress instance"

+++
# Import Yootheme demo content to aws lightsail wordpress instance

1) Lauch aws light sail instance

2) connect via ssh

3) backup existing config on server: sudo cp \~/apps/wordpress/htdocs/wp-config.php \~/wp-config.php.bck

3) copy demo folder, example: scp \~/lilian_demo_package_wp.zip bitnami@18.14.78.39:/home/bitnami/upload.zip

4) delete old installation: sudo rm -rf \~/apps/wordpress/htdocs/

5) unzip: sudo unzip upload.zip -d \~/apps/wordpress/

6) rename to htdocs: sudo mv \~/apps/wordpress/lilian_demo_package_wp \~/apps/wordpress/htdocs

7) sudo cp \~/wp-config.php.bck \~/apps/wordpress/htdocs/wp-config.php

8) sudo chown -R bitnami \~/apps/wordpress/htdocs/