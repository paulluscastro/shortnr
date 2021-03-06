# Shortnr **A URL Shortener**

The solution is made of 2 projects: a WEB API, which publicly available after its docker container is up, and a ASP.NET MVC interface to make it easier for the users to see statistics and send new URLs to be shortened.

Each project is distributed into a separated Docker Container and both access a single SQL Server 2017 Database which is ran on another Docker Container.

After running the project the MVC project will be available at port 62386 and the Web API will be exposed at port 54411.

The API URL that shortens URLs is: /api/v1/shorten

Redirection is made by the api: ```https://localhost:54411/{your new url}``` will redirect you to the original URL stored in the database. Additionally it will increase the number of accesses that that URL had and the last time it was accessed.


To shorten a URL just **POST** an object like this to that URL:
```json
{
	"OriginalUrl": "http://www.google.com.br",
	"LinkExpiration": 1
}
```
And your URL will be shortened. Accepted values to "LinkDuration" field:
  - 1 - One week 
  - 2 - One month
  - 3 - One Year
  - 4 - Never

After shortening you will receive an object like this:
```json
{
    "shortenedUrl": "1",
    "originalUrl": "http://www.google.com.br",
    "expiration": 0,
    "created": "2019-01-21T08:05:58.6633333",
    "lastUpdated": "2019-01-21T08:05:58.6633333",
    "accesses": 0,
    "lastAccess": null
}
```
# How to run
Download the repository, extract its contents, navigate to the folder where you extracted it (aim for the file "docker-compose.yml") and run:

```sh
docker-compose up
```
If this does not work it might be necessary to install Docker in your machine. Refer to [Docker Hub](https://www.docker.com/get-started) to download the proper installation or read the instructions to install it in your OS.
