+++
title = 'How to create secure file in linux?'
date = 2024-01-26T11:37:47-06:00
draft = false
+++

![tomb](/img/tomb.png)
If you're looking for a robust solution to secure your files on a Linux system, Tomb is an excellent tool to explore. Tomb provides a simple and effective way to create encrypted containers for your sensitive data. Follow these steps to get started:

### Install Tomb
Firstly, install Tomb on your system using the package manager. For Debian-based systems, you can use the following command:

```bash
sudo apt install tomb
```

### Create a Tomb
Now, let's create a Tomb, a secure container for your files. Replace `<filename>` with the desired name for your Tomb and `<filename.key>` with the key file name.

```bash
tomb dig -s 1000 <filename>
```

### Add Key to the Tomb
To add a key file to the Tomb, use the following command. Replace `<filename.key>` with the key file name.

```bash
tomb forge <filename.key> -f
```

### Lock the Tomb
Once you have added the key, lock the Tomb to secure your files.

```bash
tomb lock <filename> -k <filename.key>
```

### Open the Tomb
When you need to access your secure files, open the Tomb using the key.

```bash
tomb open <filename> -k <filename.key> -f
```

### Close the Tomb
After you're done working with your secure files, remember to close the Tomb.

```bash
tomb close
```

> Tomb provides a straightforward yet powerful way to keep your files secure. Customize the file names and paths as needed to suit your preferences and file organization. If you're dealing with sensitive data, Tomb can be a valuable addition to your security toolkit.


Stay secure!

Anson Sarosh Dsouza