FROM node 

WORKDIR /app
# Copy package.json and package-lock.json to the working directory.
COPY package*.json ./
# Install dependencies.
RUN npm install

# Copy the rest of the source files into the image.
COPY . .
# Expose the port that the application listens on.
EXPOSE 3000

# Run the application.
CMD npm run dev
