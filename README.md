# Linux Security Lab

## Objective

This is my first Linux security lab.

## What I learned

- Basic Linux navigation
- Creating files with touch
- Reading files with cat
- Understanding Linux file permissions
- Changing permissions with chmod

## Permission Practice

I created a file called `notes.txt`.

Initial permission:

`644`

I changed it to:

`600`

This means only the file owner can read and write the file.

## Environment

- Ubuntu
- WSL 2
- Linux

## User and Permission Lab

I created a second Linux user called `labuser` to test file permissions.

### Experiment

With `notes.txt` set to `600`, `labuser` could not read the file.

I temporarily changed the file permission to `644`, but `labuser` was still denied because `/home/billi` did not allow other users to traverse it.

After temporarily adding execute permission to `/home/billi`, `labuser` could read the file because `notes.txt` was `644`.

The permissions were then restored to:

- `/home/billi`: `750`
- `notes.txt`: `600`

### Security Lesson

File permissions and directory permissions work together. A user needs appropriate directory permissions to reach a file before the file's own permissions can be evaluated.

## Authentication Log Investigation

I used `/var/log/auth.log` to investigate sudo activity.

I filtered the log with:

`sudo grep 'USER=labuser' /var/log/auth.log`

The log showed that user `billi` used `sudo` to execute `cat` as `labuser`.

The command was recorded even though `labuser` received `Permission denied` when trying to read `notes.txt`.

### Security Lesson

Authentication logs can help investigate user activity by showing:

- Who performed an action
- Which user the command ran as
- Which command was executed
- When the activity occurred

Logs are important for investigating suspicious or unauthorized activity.
