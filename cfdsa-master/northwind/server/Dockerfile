FROM node:latest
ENV DB_HOST=nwdb DB_PORT=3306 DB_USER=root DB_PASSWORD=changeit \
APP_PORT=3000 APP_DIR=/app

# create APP_DIR and cd into it 
WORKDIR ${APP_DIR}

# copy files to APP_DIR
ADD main.js .
ADD package.json .
# destination folder name must be provided for copying directory
ADD public public
ADD views views
ADD config config

# install libraries from package json
RUN npm install
# End of Docker build

# Start of Docker run
EXPOSE ${APP_PORT}

HEALTHCHECK \
--interval=60s \
--timeout=5s \
--start-period=5s \
--retries=3 \
CMD curl -f -s http://localhost:${APP_PORT}/health || exit 1

# execute the image
ENTRYPOINT [ "node", "main.js" ]

