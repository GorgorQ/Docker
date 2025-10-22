FROM postgres:17.2-alpine


# Copy initialization scripts to the entrypoint directory
COPY 01-CreateScheme.sql /docker-entrypoint-initdb.d/
COPY 02-InsertData.sql /docker-entrypoint-initdb.d/