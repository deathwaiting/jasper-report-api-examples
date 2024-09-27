# Examples for using jasper-reports API

## Setting up the environment

- Here we use a sample PostgreSQL database and an instance for the report server, with security disabled
- Database is based on [this project](https://github.com/zseta/postgres-docker-samples)
- Sample reports are saved to `./reports`, which is mounted to the report server
- The root directory can also be opened as a jasper studio workspace, and reports directory will be imported as a project.
    - So, you can open this repo in jasper studio to fiddle with sample reports if you want
    - The project will have a data-soruce for the local sample database called `local-postgres`, this is what all the reports use.
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

## Example 3: A Report book with nested subreports

- A report book that have two parts, the previous movies report and a summary page.
- Note that in the case of sub-reports, `.jasper` files must be provided and referenced in the main report.
- Sub-reports `.jrxml` files are provided here for reference only.
- Jasper studio gives the feature to add sub-reports as `.jrxml` files, and compiles them on the spot. But this is not the normal case in applications, AFAIK, the library doesn't provide this out-of-the-box.
- The report server currently doesn't auto compile sub-reports `.jrxml` files.
- parameter `JR_force-compile=true` directs the server to compile sub-reports to generate `.jasper` files for them if needed.

```shell
curl -o movie_book.pdf http://localhost:8080/report/ex3/movie_book.pdf?JR_force-compile=true
```

## Example 4: A Report in Arabic language

- To produce high quality reports in Arabic, specially in pdf format we need some tweeks
- first we need better fonts, as the fonts provided by jasper doesn't produce arabic text with good quality, and some doesn't support arabic.
- Also to show the number in hinid numerals, which are used in the Arabic language we need to use a customer `FormatFactory` and use some utils for converting numerals in strings
- In this test we use open fonts provided by google's Noto family that produces higher quality text, and to handle the numerals we use [jasperreports-arabic](https://github.com/deathwaiting/japerreports-arabic)

```shell
curl -o arabic-report.pdf http://localhost:8080/report/ex4/arabic-report.pdf
```