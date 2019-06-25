FROM node:latest

# Start of Docker build
# define environemnt variable
ENV APP_PORT=5000 APP_DIR=/fortune

# create APP_DIR and cd into it 
WORKDIR ${APP_DIR}

# copy files to APP_DIR
ADD main.js .
ADD package.json .
# destination folder name must be provided for copying directory
ADD public public
ADD views views

# install libraries from package json
RUN npm install
# End of Docker build

# Start of Docker run
EXPOSE ${APP_PORT}

# Health check to monitor container readiness
# take not the localhost and app_port is the internal address NOT external address
HEALTHCHECK \
--interval=60s \
--timeout=5s \
--start-period=5s \
--retries=3 \
CMD curl -f -s http://localhost:${APP_PORT}/health || exit 1

# execute the image
ENTRYPOINT [ "node", "main.js" ]
