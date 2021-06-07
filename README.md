# Project Name

ETL Task

## Installation

The project can be ran if one has Docker and docker-compose already available with one line: `docker-compose -f etl-task.yml up -d`. This will pull three prebuilt containers and set up everything for the user. Clone this repository with `git clone https://github.com/high1/etl-task.git`, it contains both the docker-compose file and Postman collection. You need [git](https://git-scm.com/) SCM for this.

## Usage

One of the containers that will run, **[etl-mongo](https://hub.docker.com/_/mongo/)**, is a [MongoDB](https://www.mongodb.com/) instance, so if you have another one already running localy or inside another container on the default port, 27017, stop it prior to running this. ***etl-mongo*** container will expose the database with data on the default host port, `localhost:27017`, and does not use authentication, for the sake of simplicity. [Robo 3T](https://github.com/Studio3T/robomongo/releases) is a free tool which can be used to look at the data, if you need one. 

The second container, **[etl-data-gen](https://github.com/high1/etl-data-gen)**, contains an application written in [TypeScript](https://www.typescriptlang.org/) and uses [ts-node](https://typestrong.org/ts-node/) to directly run TypeScript code, without transpiling it prior. It is exposed on a local 3000 port, and has one REST GET endpoint `http://localhost:3000/shifts` which accepts ids and from & to parameters. You can access and query it directly using [Postman](https://www.postman.com/), and a Postman collection is provided along with the docker-compose file for convenience. This container generates random data. Clone it with `git clone https://github.com/high1/etl-data-gen.git`.

The third container, **[etl-job-exec](https://github.com/high1/etl-job-exec)**, extract the data from the shifts endpoint, transforms it, and loads it in the mongo database. Uses the same technology as the previous container, and also uses [mongoose](https://mongoosejs.com/) for MongoDB access. It also exposes two REST endpoints, POST `http://localhost:4000/etl`
which uses [JSON](https://en.wikipedia.org/wiki/JSON) body for parameters that will be forwarded to the shifts REST endpoint. POST is used to denote that the action will result in an action that will change the data. Also, one REST PATCH endpoint, `http://localhost:4000/clr`, can be used to clear all the data from the database, without parameters. Everything needed to work with the REST endpoints is inside the POSTMAN collection. Clone it with `git clone https://github.com/high1/etl-job-exec.git`.


## Contributing

The code for the both containers is on GitHub, [etl-data-gen](https://github.com/high1/etl-data-gen) and [etl-job-exec](https://github.com/high1/etl-job-exec). Both repos contain everything that's needed to run or build the containers localy.

1. Fork it or clone it with `git clone` following with the URL!
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request :D

For both containers, [Visual Studio Code](https://code.visualstudio.com/) was used for development. All of the code base is linted with ESLint, and uses wide set of [ESLint](https://eslint.org/) to keep the code clean and consistent. [Prettier](https://prettier.io/) is used for code formatting. [ESLint VS Code](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) is essential for the development.

## History

Task was finished during one weekend.

## Credits

I don't think these are needed.

## License

Is there a need for one?
