# Examples for using jasper-reports API

## Setting up the environment

- Here we use a sample PostgreSQL database and an instance for the report server, with security disabled
- Database is based on [this project](https://github.com/zseta/postgres-docker-samples)
- Sample reports are saved to `./reports`, which is mounted to the report server
- To run the environment run

```shell
docker-compose up
```

- To stop the environment and clean up

```shell
docker-compose down --rmi local
```

## Example 1: Simple PDF report
- A simple report that shows list of movies from the database
- Doesn't required any other resources: fonts, sub-reports, images, etc

```shell
curl -o movies.pdf http://localhost:8080/report/ex1/movies.pdf
```

## Example 2: Report with simple resources
- Simple report but with custom fonts and static image

```shell
curl -o movies.pdf http://localhost:8080/report/ex2/movies.pdf
```