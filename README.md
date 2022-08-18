## Docker environment for analytics project


### Kafka
To start kafka locally, run command \
`docker-compose -f docker-compose-kafka.yml up -d`

Kafka starts on port 9093 without authorization\
[Kafka UI](http://0.0.0.0:9001) starts on port 9001.

### Clichouse
To start clickhouse locally, run command \
`docker-compose -f docker-compose-clickhouse.yml up -d`

Clichouse server starts on port 8123 without authorization\
[Tabix GUI](http://0.0.0.0:8124) starts on port 8124.

### Postgres
To start postgres locally, run command \
`docker-compose -f docker-compose-postgres.yml up -d`
 