# Configuration on Ubuntu
This is a notebook that I used when I took Hadoop configuration on Ubuntu.

# Add new user for Hadoop
Create one new user for Hadoop. The new user name is "hadoop"

```console
$ sudo adduser -m hadoop -s /bin/bash
```

Then we need to setup the password.

```console
$ sudo passwd hadoop
```

We need to give the `sudo` permission to the new user in order to do the following configuration.

```console
$ sudo adduser hadoop sudo
```

# Install SSH
In order to use Hadoop single node cluster, we need to use SSH and make the system updated. 

First, under the new user `hadoop`, we need to use the following command:

```console
$ sudo apt-get update
$ sudo apt-get install openssh-server
```

After we install the SSH server, we can use the following command to connect:

```console
$ ssh localhost
```

We will see that system needs the fingerprint and password, type `yes` and login. Actually, we can take some setup, then we can login without any password.

Type the following command:

```console
$ cd ~/.ssh
$ ssh-keygen -t rsa
```

Then, if you don't know what you are doing, just hit `Enter` on the keyboard. We will see the password key. We need to save this key in our permission file:

```console
$ cat ./id_rsa.pub >> ./authorized_keys
```

# Java Configuration
Because Hadoop need to use Java, we need to download and install openjdk. The Java Configuration can find one Java offical documents.

Suppose we have already finished Java configuration, then we need to adjust some environment variables.

First, open the personal setting shell file `.bashrc`:

```console
$ gedit ~/.bashrc
```

Then, add the one line at the beginning of the docs:

```
export JAVA_HOME='your java installation path'
```

**Be careful**: Don't leave blank before or after '='!

Then, we need to make the environment effective, we need to run this command:

```console
$ source ~/.bashrc
```

We can use the following commands to check if environment variables is effective:

```console
$ echo $JAVA_HOME
$ java -version
```

# Install Hadoop
We can use the [official link](https://hadoop.apache.org/releases.html) to download Hadoop. Download the file under the **Binary download**. This one is already compiled.

Then, unzip the file and save it to the `bin` directory.

```console
$ sudo tar -zxf 'your hadoop file path' -C '/usr/local'
```

Go to this folder and rename the folder:

```console
$ sudo mv ./hadoop-x.x.x/ ./hadoop
```

The `hadoop-x.x.x` is the origin name of the folder.

Then, we need to adjust the permission of this folder and check if we could use the hadoop:

```console
$ cd /usr/local
$ sudo chown -R hadoop ./hadoop

$ cd /usr/local/hadoop
$ ./bin/hadoop version
```

# Hadoop pseudo-Distributed Operation
To be continued...

