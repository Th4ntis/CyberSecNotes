# Redeemer

## Initial Scan:

![](<../../../../.gitbook/assets/image (5) (1) (3).png>)

## Task 1:

#### Which TCP port is open on the machine?

Found in initial scan

Answer: 6379

## Task 2:

#### Which service is running on the port that is open on the machine?

[Redis Website](https://redis.io/)

Answer: Redis

## Task 3:

#### What type of database is Redis? Choose from the following options: (i) In-memory Database, (ii) Traditional Database

![](<../../../../.gitbook/assets/image (3) (1) (3).png>)

Answer: in-memory Database

## Task 4:

#### Which command-line utility is used to interact with the Redis server? Enter the program name you would enter into the terminal without any arguments.

[Redis-CLI Docs](https://redis.io/docs/manual/cli/)

Answer: Redis-CLI

## Task 5:

#### Which flag is used with the Redis command-line utility to specify the hostname?

[Redis-CLI Docs](https://redis.io/docs/manual/cli/)

Answer: -h

## Task 6:

#### Once connected to a Redis server, which command is used to obtain the information and statistics about the Redis server?

[REDIS info](https://redis.io/commands/info/)

Answer: info

## Task 7:

#### What is the version of the Redis server being used on the target machine?

Found from initial scan

Answer: 5.0.7

## Task 8:

#### Which command is used to select the desired database in Redis?

[Redis Select](https://redis.io/commands/select/)

Answer: SELECT

## Task 9:

#### How many keys are present inside the database with index 0?

Run INFO

![](<../../../../.gitbook/assets/image (4) (1) (1) (1).png>)

Answer: 4

## Task 10:

#### Which command is used to obtain all the keys in a database?

Google: redis command to obtain all the keys in a database

Answer: keys \*

## Task 11:&#x20;

#### Submit root flag

![](<../../../../.gitbook/assets/image (9) (1).png>)

Answer: 03e1d2b376c37ab3f5319922053953eb
