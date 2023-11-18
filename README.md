# notes-app-back-end

The purpose of creating this application is to serve as a learning resource for developing a Restful API using the Hapi framework, utilizing the PostgreSql database management system, integrating a Message Broker with RabbitMq, and implementing server-side caching with Redis.

## Tech Stack
- **Server :** Nodejs with Hapi Framework, RabbitMQ, Redis/Memurai

## Run Locally

Clone the project

```bash
  git clone https://github.com/khalilannbiya/notes-app-back-end.git
```

Or Download ZIP

[Link](https://github.com/khalilannbiya/notes-app-back-end/archive/refs/heads/main.zip)

Go to the project directory

```bash
  cd notes-app-backend
```

Install the package using the following command:
```bash
  pnpm i 
```

Copy and paste the .env file using the command:

```bash
  cp .env.example .env
```

Let's Configure the .env file

- For the PORT and HOST to run the Hapi server, here's an example: https://hapi.dev/tutorials/?lang=en_US#-creating-a-server
- For PGUSER to PGPORT, it's the PostgreSQL database configuration. Make sure PostgreSQL is installed on your local machine. You can follow these steps: https://www.w3schools.com/postgresql/postgresql_install.php. Here's an example:
   ```bash
   PGUSER=pengembang // Make sure you have created the 'pengembang' user in PostgreSQL
   PGHOST=localhost // The host for PostgreSQL can vary depending on where the PostgreSQL server is hosted. If PostgreSQL is hosted on your local machine (localhost), you can use localhost or 127.0.0.1 as the host. However, if PostgreSQL is hosted on an external server or in the cloud, you should use the IP address or hostname of that server
   PGPASSWORD=veryhardpassword // Provide a strong password and make sure you remember it
   PGDATABASE=notesapp // Fill in the database you want to use and make sure the database has been created
   PGPORT=5432 // Also, make sure to check the port used by the PostgreSQL server (default is 5432)
  ```
- For ACCESS_TOKEN_KEY and REFRESH_TOKEN_KEY, there's something you need to know first. For the JWT token key values, never set them to easily guessable or weak security values. If someone manages to obtain these keys, they can create or manipulate valid tokens without going through the system. Since JWT stores user identities in the token, they could become anyone, even an admin. So, provide values that are not easily known and random. Also, for added security, make ACCESS_TOKEN_KEY and REFRESH_TOKEN_KEY different. For security, let's generate a random string using the following command in the node REPL:
  ```bash
  require('crypto').randomBytes(64).toString('hex')
  ```
- For ACCESS_TOKEN_AGE, it represents the validity period of the access token. The faster it expires, the better. In my case, it is set to 30 minutes in seconds
- For RABBITMQ_SERVER, it is for configuring the Message Broker. In this case, Rabbit MQ is used. Make sure your machine already has Rabbit MQ installed. You can follow the installation guide here: [link](https://medium.com/geekculture/installing-rabbitmq-on-windows-4411f5114a84)
- For REDIS_SERVER, it is for configuring Redis. Make sure Redis is installed. Note that Redis officially stopped supporting Windows. However, for Windows users, there is an alternative engine that can be used as a caching memory, namely Memurai. Even though we are not using Redis directly, Memurai uses the Redis source code that has been ported to support running on Windows. So, there is almost no difference in terms of using Memurai compared to Redis, both in terms of using the command-line and in application development using the SDK. We can even refer to the documentation provided by Redis even if we use Memurai. To download and install Memurai on Windows, please visit the Memurai download page: [link](https://www.memurai.com/get-memurai) and install it using the following steps: [link](https://docs.memurai.com/en/installation). Alternatively, you can install Redis by enabling WSL with the following steps: [link](https://redis.io/docs/install/install-redis/install-redis-on-windows/)

Run the migration table with the command:
```bash
  pnpm run migrate up
```

Since we are using a Message Broker, and this project is a producer, don't forget to clone the project https://github.com/khalilannbiya/notes-app-queue-consumer.git as a consumer, then follow the installation steps in the project's repository. And, remember to run them simultaneously after setting up the projects to avoid any errors.

Make sure that the PostgreSQL server, RabbitMQ, and Redis/Memurai servers are already running.

Run the server:
```bash
  pnpm run start-dev
```

## Documentation

- [Nodejs](https://nodejs.org/en)
- [Hapi](https://hapi.dev/)
- [Redis](https://redis.io/)
- [Memurai](https://www.memurai.com/)
- [Rabbit MQ](https://www.rabbitmq.com/)
- [Mengapa Message Broker](https://medium.com/@acep.abdurohman90/mengapa-menggunakan-message-broker-c17453cb225e)

## Feedback

If you have any feedback, please reach out to us at syeichkhalil@gmail.com
