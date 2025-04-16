
#STEP 5: REDIS SERVICE FOR CACHING

# Link Extractor: Step 5

A web application to extract links and anchor texts from a given web page and analyze link statistics.

## Changes from the previous step

* Another `Dockerfile` is added for the PHP web application to avoid live file mounting
* A Redis container is added for caching using the official Redis Docker image
* The API service talks to the Redis service to avoid downloading and parsing pages that were already scraped before

## Try it out

```
$ docker-compose up --build
```

Open http://localhost/?url=http%3A%2F%2Fodu.edu%2F in a web browser.

To check whether or not the Redis service is being utilized, we can use docker-compose exec 
followed by the redis service name and the Redis CLI’s monitor command:

```
docker-compose exec redis redis-cli monitor
```

Now that we are not mounting the /www folder inside the container, local changes should not 
reflect in the running service:

```
sed -i 's/Link Extractor/Super Link Extractor/g' www/index.php
```

Verify that the changes made locally do not reflect in the running service by reloading the 
web interface and then revert changes:

```
git reset --hard
```

Now, shut these services down and get ready for the next step:

```
docker-compose down
```

Press `Ctrl + C` to terminate the service.
