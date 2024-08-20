## 10.07.2024

# DRF-with-celery-redis-flower

This commands are used to activate celery, redis, and flower on django, djangorestframework, first always activate your `env` file, then run your project using the below command

```CommandPrompt
python manage.py runserver
```

To run the celery worker open new terminal with current environment activate and on the same directory, and run the below command

```CommandPrompt
celery -A <your_project_name> worker -l info
```

To run the celery beat open new terminal on the same directory with environment activate, and run the below command

```CommandPrompt
celery -A <your_project_name> beat -l info
```

Then start the `redis-server` on new terminal with environment activate on the same directory, for that run the below command

> [!NOTE]
> I am using ubuntu 24.04 and used snap for installing redis and redisinsight
> If you're using MacOS, windows, or other linux distro please read the documentation on redis website

for running the redis-server on my ubuntu machine

```CommandPrompt
redis-server --port 6380 --replicaof 127.0.0.1 6379 
```

The command will starts a new Redis instance using port 6380 as a replica of the instance running at 127.0.0.1 port 6379. After all this to monitor celery I'm using `Flower` so run the below command (terminal with `env` activate on the same directory) to open the `Flower` dashboard.

```CommandPrompt
celery -A <your_project_folder> flower --broker:redis://
```

Then navigate to [http://127.0.0.1:5555/](http://127.0.0.1:5555/) for monitoring celery tasks using flower

> [!NOTE]
> use `celery -A <project_name> purge` to remove all tasks

> [!TIP]
> Here i'm redis as my `broker-agent` if your using anyother platform please read the documentation for flower

## 11.07.2024

# Git & Markup Language

> For the git error [rejected] master -> master (fetch first)
 
**Reference** : [Click on this link and refer the github gist](https://gist.github.com/sharbel93/ebcf0b18782573f4d95f80caa3c84acb#file-how-to-solve-this-problem-of-rejected-master-master-fetch-first)

> Markuplanguage reference links for customize your markdown documents

**Reference** : [Git gist link](https://gist.github.com/pvrego/2e346674c3abbaa6366dfe86b8488dc9), [Stackoverflow link](https://stackoverflow.com/questions/11509830/how-to-add-color-to-githubs-readme-md-file), [Git community discussion link](https://github.com/orgs/community/discussions/16925), [Git documentation](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#alerts)


## 09.08.2024

# Networking

- `nslookup` - Used to find the ip of a domain
  
  ```CommandPrompt
  nslookup example.com
  ```

- `dig` - Used to find the informations asbout the domain

  ```CommandPrompt
  dig example.com
  ```

- `whois` - Used to get the network information

  ```CommandPrompt
  whois <ip_address?
  ```

- `ipcalc` - To calculate the ip address range manually

  ```CommandPrompt
  ipcalc <ip_address>
  ```

> [!NOTE]
> You have to install `ipcalc` for that use the below command:

```CommandPrompt
sudo apt-get install ipcalc
```

- `nmap -sn` - To find specific network range live hosts

  ```CommandPrompt
  nmap -sn <ip_address>
  ```

- `nmap -p- `- Command to find the ip addresses ports

  ```CmmandPrompt
  nmap -p- <ip_address>
  ```

- `nmap -sV` - Command to find the ip address versions

  ```CommandPrompt
  nmap -sV <ip_address>
  ```


## 14.08.2024
# Image Annotation Tools

- [LabelImg](https://pypi.org/project/labelImg/) : A popular open-source graphical image annotation tool. It supports the drawing of bounding boxes for object detection tasks.
  
- [VGG Image Annotator](https://www.robots.ox.ac.uk/~vgg/software/via/via_demo.html) : An open-source web-based tool developed by the Visual Geometry Group at the University of Oxford.
  
- [CVAT (Computer Vision Annotation Tool)](https://www.cvat.ai/) : An open-source, web-based tool developed by Intel. Designed for professional use, CVAT supports a wide variety of annotation tasks.

- [Labelbox](https://labelbox.com/) : A commercial annotation platform that provides a suite of tools for labeling images, videos, and text.

- [RectLabel](https://rectlabel.com/) : A MacOS application for labeling images, primarily supporting bounding box annotation.

- [SuperAnnotate](https://www.superannotate.com/) : A platform that combines annotation tools with project management capabilities.

- [MakeSense.AI](https://www.makesense.ai/) : A free, web-based annotation tool supporting various types of annotations.

- [Roboflow](https://roboflow.com/) : A tool that not only provides annotation capabilities but also helps manage datasets and preprocess images for machine learning.

> [!TIP]
> Use the above tools for creating annotated image dataset

# Django Framework

To create an app inside a particular folder like below

```
project_folder
    |
    |__ folder_1/sub_folder
            |
            |__ app_folder
```

Use the below command

```bash
python manage.py <app_folder> folder_1/sub_folder/app_folder/
```

> [!NOTE]
> First you have to create the app folder before creating the app manually

## 20.08.2024
# How to use pip packages on intranet (a private network)

***STEP 1:***

First on a machine with internet access download the dependencies using `pip`

***syntax:***

```bash
pip download <package-name> -d <directory-path>
```

***Example:***

I want to download the `pandas` library inside the directory `packages-and-libraries`, the command will be like this:

```bash
pip download pandas -d packages-and-libraries/
```

The above command will download the `pandas` library inside the `packages-and-libraries` directory.

***STEP 2:***

Transfer the directory that contains download packages to the offline machine

> [!NOTE]
> Use any data transfer medium that doesn't require internet access and allowed by your organization

***STEP 3:***

Create and activate a virtual environment to install the packages and libraries

> [!NOTE]
> Using a virtual environment is not strictly necessary, but it is highly recommended when installing and running packages and libraries, especially in offline scenarios.

To create a virtual environment use the below command:

```bash
python -m venv <your-virtual-environment-name>
```

To `activate` virtual environment on ***windows***, use the below command:

```bash
<your-venv>\Scripts\activate
```

On ***Linux/macOS***

```bash
source <your-venv>/bin/activate
```

***STEP 4:***

Install the packages that you already downloaded using the below command:

***Syntax:***

```bash
pip install --no-index --find-links=<your-download-directory>/ <package-name>
```

***Example:***

On the above example we download the `pandas` library inside the `packages-and-libraries` directory. So, to install the `pandas` the command will be look like this:

```bash
pip install --no-index --find-links=packages-and-libraries/ pandas
```

If you want to install the dependencies using `requirements.txt` file you can use the below command:

```bash
pip install --no-index --find-links=<your-download-dir>/ -r requirements.txt
```
