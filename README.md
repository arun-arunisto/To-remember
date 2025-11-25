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
or
if the above command didn't work, use the below command:
```
celery -A <your_project_name> worker --pool=threads --concurrency=16 -l info
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

(Additional information (14/10/2025) - for getting the result in flower dashboard, return the result value inside the tasks functions)


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

## 10.09.2024

Migrations on django for different scenario

***First Scenario:*** To migrate all the contents of your project use:

```Python
Python manage.py makemigrations
```

After that,

```Python
python manage.py migrate
```

***Second Scenario:*** If you want to migrate only from a particular app use the below command

```Python
python manage.py makemigrations <app-name>
```

After that,

```Python
python manage.py migrate <app-name>
```
***Example:*** If i have an app named `blogs` and i want to migrate the models from that app.

```Python
python manage.py makemigrations blogs
```

After that same for `migrate` command also

```Python
python manage.py migrate blogs
```

***Third Scenario:*** If i want to migrate a particular migration file from a particular app

```Python
python manage.py makemigrations <app-name>
```

And if you make migrations it will create a python file on your `app`'s migrations directory, so you can use that filename to migrate, like below

```Python
python manage.py migrate <app-name> <file>
```
***Example:*** i have an app named `blogs` and i want to migrate a particular migrations file from the app, it will look like below

```Python
python manage.py makemigrations blogs
```
After makemigrations it will create files like `0001_initial.py` on your migrations folder on your app folder so you have to migrate using the file like below

```Python
python manage.py migrate blogs 0001
```

> [!TIP]
> If you're getting errors while using `migrate` command you can check the ***sqlqueries*** using `python manage.py sqlmigrate <app-name> <file>`


## 20.09.2024

# Daemonising Django, Celery & Celery Beat

## Django

#### Step 1: Create a `systemd` Service File

Create a new service file for your Django project. Open a terminal and run:

```bash
sudo nano /etc/systemd/system/django.service
```

Add the following content:

```ini
[Unit]
Description=Django Application
After=network.target

[Service]
User=your_user
Group=your_group
WorkingDirectory=/path/to/your/django/project
ExecStart=/path/to/your/virtualenv/bin/gunicorn --workers 3 --bind 0.0.0.0:8000 \
          your_project_name.wsgi:application
Restart=always

[Install]
WantedBy=multi-user.target
```

Replace the placeholders:
- `your_user` – Your system's username.
- `your_group` – Your system's group name (often the same as your username).
- `/path/to/your/django/project` – The full path to your Django project directory.
- `/path/to/your/virtualenv` – The full path to your virtual environment.
- `your_project_name` – The name of your Django project.

This example uses **Gunicorn** as the application server. Ensure Gunicorn is installed in your virtual environment if you're using it:

```bash
pip install gunicorn
```

#### Step 2: Reload `systemd` and Start the Service

Reload the `systemd` daemon and start your Django service:

```bash
sudo systemctl daemon-reload
sudo systemctl start django
```

To enable Django to start automatically when the system boots:

```bash
sudo systemctl enable django
```

You can check the status of your Django service with:

```bash
sudo systemctl status django
```

#### Step 3: Allow Port 8000 (Optional)

If you're running your Django project on port 8000 and using a firewall like `ufw`, you may need to open the port:

```bash
sudo ufw allow 8000
```

## Celery

#### Step 1: Create Celery Service File

Create a new `systemd` service file for Celery:

```bash
sudo nano /etc/systemd/system/celery.service
```

Add the following configuration to the file:

```ini
[Unit]
Description=Celery Service
After=network.target

[Service]
Type=forking
User=your_user
Group=your_group
WorkingDirectory=/path/to/your/project
ExecStartPre=/path/to/your/virtualenv/bin/celery -A your_project_name purge -f
ExecStart=/path/to/your/virtualenv/bin/celery -A your_project_name worker --loglevel=INFO
ExecStop=/path/to/your/virtualenv/bin/celery multi stop worker --pidfile=/path/to/pid/celery.pid
ExecReload=/path/to/your/virtualenv/bin/celery multi restart worker --pidfile=/path/to/pid/celery.pid

[Install]
WantedBy=multi-user.target

```

Replace the following placeholders:
- `your_user` – Your system username.
- `your_group` – Your system user group.
- `/path/to/your/project` – The path to your Django project.
- `/path/to/your/virtualenv` – The path to your virtual environment.
- `your_project_name` – The name of your Django project.

#### Step 2: Reload and Start the Service

Reload the `systemd` daemon and start the Celery service:

```bash
sudo systemctl daemon-reload
sudo systemctl start celery
```

To enable Celery to start on boot:

```bash
sudo systemctl enable celery
```

You can check the status of the Celery service with:

```bash
sudo systemctl status celery
```

## Celery Beat

#### Step 1: Create a `systemd` Service File for Celery Beat

Create a new service file for Celery Beat:

```bash
sudo nano /etc/systemd/system/celerybeat.service
```

Add the following configuration:

```ini
[Unit]
Description=Celery Beat Service
After=network.target

[Service]
User=your_user
Group=your_group
WorkingDirectory=/path/to/your/django/project
ExecStart=/path/to/your/virtualenv/bin/celery -A \
          your_project_name beat --loglevel=INFO \
          --pidfile=/var/run/celerybeat.pid
Restart=always

[Install]
WantedBy=multi-user.target
```

Replace the placeholders:
- `your_user`: The system user that will run the service.
- `your_group`: The group of the system user.
- `/path/to/your/django/project`: The absolute path to your Django project.
- `/path/to/your/virtualenv`: The absolute path to your virtual environment.
- `your_project_name`: Your Django project name.

#### Step 2: Reload `systemd` and Start the Service

After creating the service file, reload `systemd` and start the Celery Beat service:

```bash
sudo systemctl daemon-reload
sudo systemctl start celerybeat
```

To ensure that Celery Beat starts on system boot:

```bash
sudo systemctl enable celerybeat
```

Check the status of the service:

```bash
sudo systemctl status celerybeat
```

## 26.09.2024

To kill the port in ubuntu

```bash
sudo kill -9 `sudo lsof -t -i:9001`
```
If this not working try this method

```bash
sudo kill -9 $(sudo lsof -t -i:9001)
```

## 30.09.2024

To configure **Gunicorn** for serving your Django application in a production environment, follow these steps:

### 1. **Install Gunicorn**

First, install Gunicorn in your Django project environment:

```bash
pip install gunicorn
```

You can add it to your `requirements.txt` or `pyproject.toml` file to ensure it gets installed whenever the project is set up.

### 2. **Running Gunicorn Locally (for testing)**

You can start Gunicorn to serve your Django project by running:

```bash
gunicorn myproject.wsgi:application
```

Here:
- `myproject` is the name of your Django project folder where the `wsgi.py` file is located.
- `application` refers to the WSGI application callable in `myproject/wsgi.py`.

This command starts a basic Gunicorn server that serves your Django app.

### 3. **Configuring Gunicorn with Options**

To properly configure Gunicorn for production, you'll need to pass some options. These include the number of worker processes, the host and port, and logging configurations.

A basic command with options might look like this:

```bash
gunicorn --workers 3 --bind 0.0.0.0:8000 myproject.wsgi:application
```

- **`--workers 3`**: Specifies the number of worker processes (a good rule of thumb is 2x the number of CPU cores).
- **`--bind 0.0.0.0:8000`**: Specifies the host and port where Gunicorn will listen.
- **`myproject.wsgi:application`**: This points to the WSGI application in your Django project.

### 4. **Advanced Configuration with a Gunicorn Configuration File**

You can create a configuration file to store all your settings, which makes management easier. This file can be a Python file.

Create a `gunicorn_config.py` file in the root of your project with the following content:

```python
# gunicorn_config.py

bind = "0.0.0.0:8000"  # Address to bind Gunicorn to
workers = 3  # Number of worker processes
accesslog = "-"  # Log access to stdout (for easy debugging)
errorlog = "-"  # Log errors to stdout (for easy debugging)
loglevel = "info"  # Log level: "debug", "info", "warning", "error", "critical"
timeout = 120  # Request timeout in seconds
```

Then, run Gunicorn with the config file:

```bash
gunicorn -c gunicorn_config.py myproject.wsgi:application
```

### 5. **Configuring Gunicorn as a Systemd Service (for Automatic Start)**

If you're using an Ubuntu server or a system that supports `systemd`, it's a good practice to configure Gunicorn to run as a service that starts on boot. Here’s how you can do that:

1. **Create a Gunicorn Service File:**

   Create a file at `/etc/systemd/system/gunicorn.service` with the following content:

   ```ini
   [Unit]
   Description=gunicorn daemon for Django project
   After=network.target

   [Service]
   User=your_username
   Group=www-data
   WorkingDirectory=/path/to/your/project
   ExecStart=/path/to/your/venv/bin/gunicorn --workers 3 --bind unix:/path/to/your/project.sock myproject.wsgi:application

   [Install]
   WantedBy=multi-user.target
   ```

   - **`User`**: The user under which the service runs (replace `your_username` with your server’s user).
   - **`WorkingDirectory`**: The full path to your Django project.
   - **`ExecStart`**: The command to start Gunicorn (with full paths to the virtual environment and project).
   - **`/path/to/your/project.sock`**: This is a Unix socket file Gunicorn will use. Nginx can connect to it.

2. **Start and Enable the Gunicorn Service:**

   After creating the service file, reload systemd, start Gunicorn, and enable it to run at boot:

   ```bash
   sudo systemctl daemon-reload
   sudo systemctl start gunicorn
   sudo systemctl enable gunicorn
   ```

3. **Check the Status of the Service:**

   You can check whether Gunicorn is running correctly:

   ```bash
   sudo systemctl status gunicorn
   ```

### 6. **Configuring Nginx to Work with Gunicorn**

Once Gunicorn is configured, you can set up Nginx as a reverse proxy to handle requests. Nginx will serve static files and forward requests to Gunicorn.

Here’s a basic Nginx configuration for serving a Django project:

1. **Install Nginx:**

   ```bash
   sudo apt update
   sudo apt install nginx
   ```

2. **Create a Nginx Server Block:**

   Create a new configuration file for your site at `/etc/nginx/sites-available/myproject`:

   ```nginx
   server {
       listen 80;
       server_name your_domain_or_IP;

       location / {
           proxy_pass http://unix:/path/to/your/project.sock;
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
           proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
           proxy_set_header X-Forwarded-Proto $scheme;
       }

       location /static/ {
           alias /path/to/your/project/static/;
       }

       location /media/ {
           alias /path/to/your/project/media/;
       }

       # Add SSL configuration if using HTTPS
   }
   ```

3. **Enable the Nginx Configuration:**

   Create a symbolic link to enable the configuration:

   ```bash
   sudo ln -s /etc/nginx/sites-available/myproject /etc/nginx/sites-enabled
   ```

4. **Test the Nginx Configuration:**

   Make sure there are no syntax errors in the configuration:

   ```bash
   sudo nginx -t
   ```

5. **Restart Nginx:**

   After confirming that the configuration is correct, restart Nginx to apply the changes:

   ```bash
   sudo systemctl restart nginx
   ```

### 7. **Final Steps:**
- Ensure you’ve collected static files (`python manage.py collectstatic`).
- Make sure your Django `ALLOWED_HOSTS` includes your domain or IP address.
- Secure your site by configuring SSL certificates (e.g., with Let’s Encrypt).

Once these steps are completed, your Django app should be ready and running behind Nginx with Gunicorn!

## To check the GPU

```Python
import torch
import torchvision

print("Torch version:", torch.__version__)
print("Torchvision version:", torchvision.__version__)
print("CUDA available:", torch.cuda.is_available())
print("CUDA version:", torch.version.cuda)
```
---
# 24.04.2025 
---

### 📘 DateTime Difference Calculation

---

#### 🕒 Example Datetimes

```python
start_datetime = '2017-05-04 08:00:00'
end_datetime = '2017-05-04 09:30:00'
```

---

### 📐 Step 1: Convert Strings to `datetime` Objects

Use Python's `datetime.strptime()` to convert string to `datetime`.

```python
from datetime import datetime

start = datetime.strptime(start_datetime, '%Y-%m-%d %H:%M:%S')
end = datetime.strptime(end_datetime, '%Y-%m-%d %H:%M:%S')
```

---

### 🧮 Step 2: Calculate Time Difference

```python
difference = end - start
```

This returns a `timedelta` object.

---

### 📏 Step 3: Convert to Seconds, Minutes, Hours

#### 🧾 Total Seconds

```python
total_seconds = difference.total_seconds()
```

#### 🧾 Total Minutes

```python
total_minutes = total_seconds / 60
```

#### 🧾 Total Hours

```python
total_hours = total_seconds / 3600
```

---

### ✅ Final Output

For the above example:

```text
Seconds: 5400.0
Minutes: 90.0
Hours: 1.5
```

---

## To check port is running or not

#### ✅ On **Linux/macOS**:
```bash
sudo lsof -i :<port_number>
```
Example:
```bash
sudo lsof -i :8000
```

Or:
```bash
netstat -tuln | grep :<port_number>
```

Or with `ss` (faster replacement for netstat):
```bash
ss -tuln | grep :<port_number>
```

#### ✅ On **Windows**:
```cmd
netstat -a -n | findstr :<port_number>
```

Example:
```cmd
netstat -a -n | findstr :8000
```
---
## 07.05.2025
### Git Fetch & Merge

```bash
git fetch origin <branch-name>
```
After fetching 
```bash
git merge <orgin-branch-name-from-the-logs>
```
---
## 16.05.2025

To restore the postgresql .sql file

```bash
psql -U <username> -d <yiur_database_name> -f <path_to_sql_file>
```
If it didnt work try with this
```bash
pg_restore -U <username> -d <your_db_name> <path_to_sql_file>
```
Again if youre facing some issues add flag verbose like below
```bash
pg_restore -U <username> -d <your_db_name> --clean --no-owner -v <path_to_your_sql>
```
----
## 02.07.2025
## Linux Commands 

To find file who’s content is in Human Readable format. This check can be performed using the `file` command. File command returns the type of data that is found in the file

```bash
file ./*
```
---

To search for the file that we require using the properties that are specified in the question we can make use of the find command.

```bash
find . -type f -size 1033c -not -executable -exec file {} + | grep ASCII
```

### Command Explanation
* . : Search the current working directory only
* -type f : Look for files only (Exclude Directories)
* -size 1033c : Look for files that are exactly 1033 bytes in size (Find uses “c” to represent bytes)
* -not -executable : Find only non executable files
* -exec file {} + : Execute the file command on all the results returns by find

**Note : {}** is an placeholder for the location where the names of the files found by find is going to be substituted. The “+” sign is used to terminate the statement

---

Since we don't know where the file is we will have to search the entire server. We know some properties about the file that we can use to try and locate the file.

```bash
find / -type f -user bandit7 -group bandit6 -size 33c
```

### Command Explanation
* / : Search the entire server (/ is the root directory on Linux similar to the C:/ Drive on Windows)
* -type f : Search only for files (Exclude Directories)
* -user bandit7 : Search for files which are owned by user bandit7
* -group bandit6 : Search for files that belongs to the group bandit6
* -size 33c : Look for files that are exactly 33 bytes in size (Find uses “c” to represent size in bytes)

This command alone is sufficient to get the result that we are looking for but since we are scanning the entire server we are going to encounter files what we do not have permission. It will raise an *permission denied* error:

These errors can be filtered out by sending the error stream denoted by number `2` to `/dev/null` . NULL is a special device on Linux which destroys all that data that is send to it.

```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2> /dev/null
```

---

`head` and `tail` command we used to get the first or last lines data from txt file like below:

```bash
head -n 10 data.txt
```

---

We know the password is next to the word “millionth” in the file. We can look for this pattern by using the `grep` command:

```bash
grep millionth data.txt 
```

---

```bash
cat data.txt | sort | uniq -u
```

Use `uniq` command with the `-u` flag to print the unique line. Uniq command expects the repeating (similar) lines to be next to each other (adjacent) so we need to sort our data before we can find the unique line.

For sorting we can use the `sort` command which will `sort` the data in the file line wise. Finally we can combine all these commands together into an one liner using the `|` (pipe) operator

---

```bash
cat data.txt | strings -e s | grep ==
```

Human readable string in an file can be found using the `strings` command. The `-e` flag is used to specify the character encoding. We are assuming the human readable line is ASCII text so we use “s” for the encoding type.

We also know that the line with the password starts with a few “=” characters. We can look for this pattern in the file using the `grep` command.

___

```bash
cat data.txt | base64 -d
```

Decoding this data using the `base64` command that is present on *nix systems. The `-d` flag is used to decode the data.

---

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

The `tr` command is used to translate/ transform data from one form to another.

---

## 10.09.2025

Connecting local postgresql server to another machine in the same netwrok.

### On the Server Machine (where postgresql is running):

1. Allow postgresql to listen all ips:

   - Open the PostgreSQL config file (postgresql.conf). (Here i am using ubuntu machine. location of the file depends on the os)

   ```bash
   /etc/postgresql/<version>/main/postgresql.conf     # Ubuntu/Debian
   ```

   - find the line.

   ```bash
   #listen_addresses = 'localhost'
   ```

   - change the line.

   ```bash
   listen_addresses = '*'
   ```

   - save and exit.

2. Allow connections from your network

   - Open `pg_hba.conf`, usually in the same folder as `postgresql.conf`.

   - Add a line like this (replace 192.168.1.0/24 with your network range):

   ```bash
   host    all             all             192.168.1.0/24          md5
   ```

   This will allow the machines to connect database with username and password.

3. Restart the postgresql

   ```bash
   sudo systemctl restart postgresql
   ```

---
     
