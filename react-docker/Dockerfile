FROM node:20-alpine


# create a user with permission to run the app 
# -s -> create asystem user
# -G add the user to a group

# this is done to avoid running the app as root
RUN addgroup app && adduser -S -G app app

# set the user to run the app
USER app

#set the directory to /app
WORKDIR /app

#copy package and package-lock to the working directory
#this is done before copying the rest of files to take advantage of docer cache
#if those file havenot changed,docker will use the cached dependencies
COPY package*.json ./

#sometimes the ownership of the files in working directory is change to root
USER root

RUN chown -R app:app .

USER app 
#install the dependency
RUN npm install
# copy all the file
COPY . .

# Expose the port
EXPOSE 5173

#run project
CMD npm run dev
