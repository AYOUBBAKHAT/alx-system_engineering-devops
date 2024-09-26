 0x1B. Web stack debugging #4
============================

-   By Sylvain Kalache, co-founder at Holberton School

![](https://s3.amazonaws.com/intranet-projects-files/holbertonschool-sysadmin_devops/313/frdkCrb.jpg)

Requirements
------------

### General

-   All your files will be interpreted on Ubuntu 14.04 LTS
-   All your files should end with a new line
-   A `README.md` file at the root of the folder of the project is mandatory
-   Your Puppet manifests must pass `puppet-lint` version 2.1.1 without any errors
-   Your Puppet manifests must run without error
-   Your Puppet manifests first line must be a comment explaining what the Puppet manifest is about
-   Your Puppet manifests files must end with the extension `.pp`
-   Files will be checked with Puppet v3.4

### Install `puppet-lint`

```
$ apt-get install -y ruby
$ gem install puppet-lint -v 2.1.1

```

Tasks
-----

### 0\. Sky is the limit, let's bring that limit higher

mandatory

In this web stack debugging task, we are testing how well our web server setup featuring Nginx is doing under pressure and it turns out it's not doing well: we are getting a huge amount of failed requests.

For the benchmarking, we are using ApacheBench which is a quite popular tool in the industry. It allows you to simulate HTTP requests to a web server. In this case, I will make 2000 requests to my server with 100 requests at a time. We can see that 943 requests failed, let's fix our stack so that we get to 0, and remember that when something is going wrong, logs are your best friends!
**Repo:**

-   GitHub repository: `alx-system_engineering-devops`
-   Directory: `0x1B-web_stack_debugging_4`
-   File: `0-the_sky_is_the_limit_not.pp`

### 1\. User limit

#advanced

Change the OS configuration so that it is possible to login with the `holberton` user and open a file without any error message.

```
root@079b7269ec1b:~# su - holberton
-su: /etc/profile: Too many open files
-su: /home/holberton/.bash_profile: Too many open files
-su-4.3$ head /etc/passwd
-su: start_pipeline: pgrp pipe: Too many open files
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
-su-4.3$
-su-4.3$
-su-4.3$ logout
-su: /home/holberton/.bash_logout: Too many open files
-su: /etc/bash.bash_logout: Too many open files
root@079b7269ec1b:~#
root@079b7269ec1b:~#
root@079b7269ec1b:~# puppet apply 1-user_limit.pp
Notice: Compiled catalog for 079b7269ec1b.ec2.internal in environment production in 0.02 seconds
Notice: /Stage[main]/Main/Exec[change-os-configuration-for-holberton-user]/returns: executed successfully
Notice: Finished catalog run in 0.06 seconds
root@079b7269ec1b:~#
root@079b7269ec1b:~#
root@079b7269ec1b:~# su - holberton
holberton@079b7269ec1b:~$ head /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
holberton@079b7269ec1b:~$

```

**Repo:**

-   GitHub repository: `alx-system_engineering-devops`
-   Directory: `0x1B-web_stack_debugging_4`
-   File: `1-user_limit.pp`
