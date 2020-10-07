<h1 align=center><i><b>Google Cloud</b></i></h1>

<img src="https://github.com/Psingh12354/Google-Cloud-/blob/main/Qwik.png" width=100 height=100></img>

<h3 align=center><i><b>Welcome! to the Qwicklab</b></i></h3>

### Go to qwiklab here [click me](https://google.qwiklabs.com/)

### About Navigation

The **Navigation menu** is an important component of the Cloud Console—it offers quick access to the platform's services and also outlines its offerings. If you scroll through the menu, you will see that there are seven categories of Google Cloud services:

- **Compute:** houses a variety of machine types that support any type of workload. The different computing options let you decide how involved you want to be with operational details and infrastructure amongst other things.
- **Storage:** data storage and database options for structured or unstructured, relational or non relational data.
- **Networking:** services that balance application traffic and provision security rules amongst other things.
- **Cloud Operations:** a suite of cross-cloud logging, monitoring, trace, and other service reliability tools.
- **Tools:** services for developers managing deployments and application build pipelines.
- **Big Data:** services that allow you to process and analyze large datasets.
- **Artificial Intelligence:** a suite of APIs that run specific artificial intelligence and machine learning tasks on Google Cloud.

### Terminal Open

To open a terminal on google cloud find the square on top right corner like this |>'| and click there

### Auth-list

To open the auth list type this command on terminal
```
gcloud auth list
```

### Types of Access Specifier

![](https://github.com/Psingh12354/Google-Cloud-/blob/main/Google.PNG)

### Text File

```
touch text.txt
```

### List the file

```
ls
```

### Read the cloud shell

```
README-cloudshell.txt  test.txt
```

### To _open_ the file in terminal

```
nano test.txt
```
### Process to come out from nano
Press
- Control + X
- Y
- Enter

### To _read_ the file in terminal

```
cat test.txt
```

<h2 align=center><i><b>Creating a Virtual Machiene</b></i></h2>

You can list the project ID with this command:

```
gcloud config list project
```

### output

```
[core]
project = qwiklabs-gcp-44776a13dea667a6
```

## Understanding Regions and Zones
Certain Compute Engine resources live in regions or zones. A region is a specific geographical location where you can run your resources. Each region has one or more zones. For example, the us-central1 region denotes a region in the Central United States that has zones ```us-central1-a```, ```us-central1-b```, ```us-central1-c```, and ```us-central1-f```.
![](https://github.com/Psingh12354/Google-Cloud/blob/main/Region.PNG)

Resources that live in a zone are referred to as zonal resources. Virtual machine Instances and persistent disks live in a zone. To attach a persistent disk to a virtual machine instance, both resources must be in the same zone. Similarly, if you want to assign a static IP address to an instance, the instance must be in the same region as the static IP.

### Create a new instance from the Cloud Console

In this section, you'll learn how to create new pre-defined machine types with Compute Engine from the Cloud Console.

In the Cloud Console, on the top left of the screen, select **Navigation menu > Compute Engine > VM Instances:**

![](https://github.com/Psingh12354/Google-Cloud/blob/main/Instance.PNG)
This may take a minute to initialize for the first time.

To create a new instance, click **Create**.

![](https://github.com/Psingh12354/Google-Cloud/blob/main/create.PNG)

There are many parameters you can configure when creating a new instance. Use the following for this lab:
![](https://github.com/Psingh12354/Google-Cloud/blob/main/instance1.PNG)
![](https://github.com/Psingh12354/Google-Cloud/blob/main/instance2.PNG)

Click **Create.**

Wait for it to finish - it shouldn't take more than a minute.

Once finished, you should see the new virtual machine in the **VM Instances** page.

To SSH into the virtual machine, click on **SSH** on the right hand side. This launches a SSH client directly from your browser.

![](https://github.com/Psingh12354/Google-Cloud/blob/main/SSh.PNG)

## Install a NGINX web server
Now you'll install NGINX web server, one of the most popular web servers in the world, to connect your virtual machine to something.

Once SSH'ed, get ```root``` access using ```sudo```:
```
sudo su -
```
As the ```root``` user, update your OS:
```
apt-get update
```
(Output)
```
Get:1 http://security.debian.org stretch/updates InRelease [94.3 kB]
Ign http://deb.debian.org strech InRelease
Get:2 http://deb.debian.org strech-updates InRelease [91.0 kB]
...
```
### Install NGINX:
```
apt-get install nginx -y
```
(Output)
```
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
...
```
### Check that NGINX is running:
```
ps auwx | grep nginx
```
(Output)
```
root      2330  0.0  0.0 159532  1628 ?        Ss   14:06   0:00 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
www-data  2331  0.0  0.0 159864  3204 ?        S    14:06   0:00 nginx: worker process
www-data  2332  0.0  0.0 159864  3204 ?        S    14:06   0:00 nginx: worker process
root      2342  0.0  0.0  12780   988 pts/0    S+   14:07   0:00 grep nginx
```
Awesome! To see the web page, go to the Cloud Console and click the External IP link of the virtual machine instance. You can also see the web page by adding the ```External``` IP to ```http://EXTERNAL_IP/``` in a new browser window or tab.
![](https://github.com/Psingh12354/Google-Cloud/blob/main/SSh.PNG)

You should see this default web page:

![](https://github.com/Psingh12354/Google-Cloud/blob/main/ngins.PNG)

To check your progress in this lab, click Check my progress below. A checkmark means you're on track.

### Create a new instance with gcloud

Rather than using the Cloud Console to create a virtual machine instance, you can use the command line tool gcloud, which is pre-installed in Google Cloud Shell. Cloud Shell is a Debian-based virtual machine loaded with all the development tools you'll need (gcloud, git, and others) and offers a persistent 5GB home directory.

In the Cloud Shell, create a new virtual machine instance from the command line using ```gcloud```:
```
gcloud compute instances create gcelab2 --machine-type n1-standard-2 --zone us-central1-c
```
(Output)
```
Created [...gcelab2].
NAME     ZONE           MACHINE_TYPE  ...    STATUS
gcelab2  us-central1-c  n1-standard-2 ...    RUNNING
```
The instance created has these default values:

- The latest Debian 9 (stretch) image.
- The n1-standard-2 machine type. In this lab you can select one of these other machine types if you'd like: n1-highmem-4 or n1-highcpu-4. When you're working on a project outside of Qwiklabs, you can also specify a custom machine type.
- A root persistent disk with the same name as the instance; the disk is automatically attached to the instance.
Run ```gcloud compute instances create --help``` to see all the defaults.
```
Note: You can set the default region and zones that gcloud uses if you are always working within one region/zone and you don't want to append the --zone flag every time. Do this by running these commands :

gcloud config set compute/zone ...

gcloud config set compute/region ...
```
To exit help, press **Ctrl+c**.

Check out your instances. Select **Navigation menu > Compute Engine > VM instances.** You should see the 2 instances you created in this lab.

![](https://github.com/Psingh12354/Google-Cloud/blob/main/SSh.PNG)

a new gcelab added here

Finally, you can SSH into your instance using ```gcloud``` as well. Make sure you add your zone, or omit the ```--zone``` flag if you've set the option globally:
```
gcloud compute ssh gcelab2 --zone us-central1-c
```
(Output)
```
WARNING: The public SSH key file for gcloud does not exist.
WARNING: The private SSH key file for gcloud does not exist.
WARNING: You do not have an SSH key for gcloud.
WARNING: [/usr/bin/ssh-keygen] will be executed to generate a key.
This tool needs to create the directory
[/home/gcpstaging306_student/.ssh] before being able to generate SSH
Keys.
```
Now you'll type **Y** to continue.
```
Do you want to continue? (Y/n)
```
**Enter** through the passphrase section to leave the passphrase empty.
```
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase)
```
After connecting, you disconnect from SSH by exiting from the remote shell:
```
exit
```
