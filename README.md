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

> [!TIP]
> Here i'm redis as my `broker-agent` if your using anyother platform please read the documentation for flower

## 11.07.2024

# Git & Markup Language

> For the git error [rejected] master -> master (fetch first)
 
**Reference** : [Click on this link and refer the github gist](https://gist.github.com/sharbel93/ebcf0b18782573f4d95f80caa3c84acb#file-how-to-solve-this-problem-of-rejected-master-master-fetch-first)

> Markuplanguage reference links for customize your markdown documents

**Reference Links** : [Git gist link](https://gist.github.com/pvrego/2e346674c3abbaa6366dfe86b8488dc9), [Stackoverflow link](https://stackoverflow.com/questions/11509830/how-to-add-color-to-githubs-readme-md-file), [Git community discussion link](https://github.com/orgs/community/discussions/16925), [Git documentation](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#alerts)

