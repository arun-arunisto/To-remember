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
```CommandPrompt
:: I am using ubuntu 24.04 and used snap for installing redis and redisinsight
:: If you're using MacOS, windows, or other linux distro please read the documentation on redis website
:: for running the redis-server on my terminal
redis-server --port 6380 --replicaof 127.0.0.1 6379 
```
The command will starts a new Redis instance using port 6380 as a replica of the instance running at 127.0.0.1 port 6379. After all this to monitor celery I'm using `Flower` so run the below command (terminal with `env` activate on the same directory) to open the `Flower` dashboard.
```CommandPrompt
celery -A <your_project_folder> flower --broker:redis://
:: here i'm using redis if your using anyother platform please read the documentation of flower 
```
