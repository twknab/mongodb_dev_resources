# Install Mongo DB On MacOS Big Sur

[TOC]



## Creating Data Folder

Before you install and use MongoDB, you need to create a data/db folder on your computer for storing MongoDB data.

## For Old OS Versions (Before Catalina)

Before macOS Catalina, you can create this folder in the user's root directory with the following command:

```
$ sudo mkdir -p /data/db
```

### Adjust permission

```
$ sudo chown -R `id -un` /data/db
```

---

## For Newer OS Versions (Catalina / Big Sur)

If you are on macOS Catalina or Big Sur (or any future release), you can not use the root folder for this purpose. macOS Catalina runs in a read-only system volume, separate from other files on the system.

Apple created a secondary volume on Catalina that you need to use for storing MongoDB data folder:

```bash
$ sudo mkdir -p /System/Volumes/Data/data/db
```

### Adjust Permission

```bash
$ sudo chown -R `id -un` /System/Volumes/Data/data/db
```

## Installing MongoDB

You can install the MongoDB community edition with Homebrew. If Homebrew is not already installed, execute the following command first:

```bash
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```


Now update Homebrew to the latest version:

```bash
$ brew update
```



Next, tap the MongoDB formulae into Homebrew:

```bash
$ brew tap mongodb/brew
```



Finally, execute the following command to install the MongoDB community edition:

```bash
$ brew install mongodb-community
```


That's it. MongoDB is now installed on your macOS computer.



---

---



## Managing MongoDB Service

To manage MongoDB on your macOS computer, you can use the brew services command.

First of all, install brew services by tapping homebrew/services:

```bash
$ brew tap homebrew/services
```

To start the MongoDB service, you use the following command:

```bash
$ brew services start mongodb-community
```



The above command will start MongoDB as a background service. Here's what you will see on the terminal:

```bash
==> Successfully started `mongodb-community` (label: homebrew.mxcl.mongodb-community)
```


Note: You can also use the run command instead of start. The start command will configure MongoDB to automatically start when you log into your Macbook. If you do not want to run MongoDB all the time, use the run command instead.

To check the current status of the MongoDB service, issue the following command:

```bash
$ brew services list
```


The above command will output something like below:

```bash
Name              Status  User       Plist
mongodb-community started forestudio /Users/forestudio/Library/LaunchAgents/homebrew.mxcl.mongodb-community.plist
redis             started forestudio /Users/forestudio/Library/LaunchAgents/homebrew.mxcl.redis.plist
```

You can stop the service anytime by typing:

```bash
$ brew services stop mongodb-community
```



If you want to restart the service, use the following command:

```bash
$ brew services restart mongodb-community
```



## Creating Aliases

To make your life easier, you can also create aliases for managing MongoDB service. Just add the following to ~/.zshrc:

- `sudo vim ~/.zshrc` -- then paste:

```
alias mongod-start="brew services run mongodb-community"
alias mongod-status="brew services list"
alias mongod-stop="brew services stop mongodb-community"
```

Next source the ~/.zshrc file to load aliases:

```
$ source ~/.zshrc
```

Now you can use aliases to manage your MongoDB service:

```
# Start MongoDB
$ mongod-start

# Check status
$ mongod-status

# Stop MongoDB
$ mongod-stop
```

***
[SOURCE](https://attacomsian.com/blog/install-mongodb-macos)