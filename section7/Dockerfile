## this is the first docker file so far that uses the multi-step docker build design pattern
## a bit more about design patterns here: https://sourcemaking.com/design_patterns
## this means this docker file is split into two phases, the build phase and the run phase

## start build phase
### the `as builder` postfix will refer to everything under the FROM step will be considered as the `builder` phase
#### using multi-stage builds only supported with docker 17.05+
FROM node:alpine as builder

WORKDIR '/usr/section6/ui'

COPY package.json .

RUN npm install

## copies all the code over after installation, no volumes logic is necessary since this is prod - files can be assumed to never change in production VM lifecycle
COPY . .

RUN npm run build
## end build phase

## start run phase - dependent on the build process from `create-react-app` being completed
### grabbing alpine version, to see if it works - not specified in the tutorial
FROM nginx:alpine

## exposes port 80 for production in AWS, exposing port 80 to utilize ngnix in prod
EXPOSE 80

### this syntax uses the --from prefix to select files from the `builder` phase established above, 
### second argument = the folder location within the specified phase' container
### third argument = the destination folder location (nginx specific syntax)
COPY --from=builder /usr/section6/ui/build /usr/share/nginx/html

### there is no need for a run command with nginx since the container image of nginx pulled from the docker server (line 23) starts itself already


### end run phase
