# db-docker
database configuration with docker-compose


## 1. MYSQL
- docker-compose
    ```yml
    version: '3.3'
    services:
    dbTestServer:
        image: mysql:5.7.26
        restart: always
        environment:
        MYSQL_DATABASE: 'db'
        # So you don't have to use root, but you can if you like
        MYSQL_USER: 'user'
        # You can use whatever password you like
        MYSQL_PASSWORD: 'password'
        # Password for root access
        MYSQL_ROOT_PASSWORD: 'password'
        ports:
        # <Port exposed> : < MySQL Port running inside container>
        - '3306:3306'
        expose:
        # Opens port 3306 on the container
        - '3306'
        # Where our data will be persisted
        volumes:
        - my-db:/var/lib/mysql
    # Names our volume
    volumes:
    my-db:
    ```
- run : `docker-compose up -d` 

---
## 2. POSTGRES
- docker-compose
    ```yml
    # docker-compose.yml
    version: '3'
    services:
    database:
        image: postgres:latest # use latest official postgres version
        env_file:
        - database.env # configure postgres
        volumes:
        - ./postgres-data:/var/lib/postgresql/data
        ports:
        - 5432:5432
    ```
- databse.env
    ```env
    # database.env
    POSTGRES_USER=bwa_laravue
    POSTGRES_PASSWORD=bwa_laravue_password
    POSTGRES_DB=bwa_laravue_shayna
    ```
- run : `docker-compose up -d`