# What

The easiest way to store data in the cloud for non-laymen (developers etc)
i.e. You should be comfortable with the command line.

# Why

As a developer I know about the different cloud storage options.
I want to be able to easily store my stuff in the cloud taking on the responsibility of payments and cloud accounts myself.

# How

## Installation

### OSX

`
brew install ....
`

### Linux

Right now you'll have to compile from source. See the dockerfiles for details.

## Set up your cloud account

You have to create your cloud accounts yourself.

Current cloud backends supported are:

- Amazon AWS

Feel free to add more!

Once you've got your cloud credentials do the following:

```
easy-storage configure backend --provider aws --aws-access-key-id $AWS_ACCESS_KEY_ID --aws-access-secret-access-key $AWS_SECRET_ACCESS_KEY --aws-region $AWS_REGION
```

Config is stored in `~/.easy-storage/config`

## Default configuration

By default the following will be setup:

Anything in `/backup` will be backed up to the cloud.

Anything in `/archive` will be archived to the cloud.

### What's the difference between `backup` and `archive`? 

Backup will create a cloud mirror of the directory. If you mutate the local directory you will mutate the cloud mirror.

Archive will "move" the files in that directory to the cloud. Local files will be deleted once the cloud transfer is complete.

Backup assumes a lot of reads and writes. Archive assumes writes but little to no reads. So for AWS it'll use s3 for backups and glacier for archives to be cost efficient.

## Custom Configuration

Most config can be done via the cli.
Feel free to hack the config file `~/.easy-storage/config` at your own risk.

### Configuring individual directories

```
# Backup a directory
easy-storage backup add .

# Stop backing up a directory
easy-storage backup rm .

# Archive a directory (NOTE: contents will be deleted after archive complete)
easy-storage archive add .

# Remove a local archive (NOTE: this leaves the cloud archive untouched for safety purposes)
easy-storage archive rm .

# Remove a cloud archive
easy-storage archive rm --cloud .

# Remove a local and cloud archive
easy-storage archive rm --all .

# List all backups
easy-storeage backup ls

# List all archives
easy-storeage archive ls

# See the status of your backup/archive
# This is hand to put in your $PS1 
easy-storeage status .

```

# Who

The bulk of development currently done by sebglazebrook. Contributors welcome!
