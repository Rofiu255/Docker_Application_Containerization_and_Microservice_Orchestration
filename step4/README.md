# wqStep 4: Link Extractor API and Web Front End Services

# Link Extractor: Step 4

A web application to extract links and anchor texts from a given web page and analyze link statistics.

## Changes from the previous step

* The link extractor JSON API service (written in Python) is moved in a separate folder
* A web front-end application is written in PHP that talks to the JSON API
* The PHP application is mounted inside the official `php:7-apache` Docker image for easier modification during the development
* The web application is accessible at `http://<hostname>[:<prt>]/?url=<url-encoded-url>`
* An environment variable `API_ENDPOINT` is used inside the PHP application to configure it to talk to the JSON API server
* A `docker-compose.yml` file is written to build various components and glue them together

## Try it out

```
$ docker-compose up --build

$ docker container ls

```
* We should now be able to talk to the API service as before:
```
$ curl -i http://localhost:5000/api/http://example.com/
```

Open http://localhost/?url=http%3A%2F%2Fodu.edu%2F in a web browser.



Now, let’s modify the www/index.php file to replace all occurrences of Link Extractor with Super Link Extractor:

```
$ sed -i 's/Link Extractor/Super Link Extractor/g' www/index.php
```

Reloading the web interface of the application (or clicking here) should now reflect 
this change in the title, header, and footer. This is happening because the ./www folder 
is bind mounted inside of the container.
This approach is very helpful in development, but in the production environment we would 
prefer our Docker images to be self-contained.

Let’s revert these changes now to clean the Git tracking:

```
git reset --hard
```
Before we move on to the next step we need to shut these services down, but Docker Compose 
can help us take care of it very easily:

```
docker-compose down
```

Press `Ctrl + C` to terminate the service.


