docker build -t hello-docer .

docker run react-docker


docker run -p 5173:5173 react-docker

docker run -p 5173:5173 -v "$(pwd):/app" -v /app/node_modules  react-docker
docker run -p 5173:5173 -v "$(pwd):/app" -v /app/node_modules -e CHOKIDAR_USEPOLLING=true react-docker

# All running container
docker ps
# All  container
docker ps -a
# Stop  container
docker stop id/name
# docker container  stop all
docker container prune


# Explaination of docker run -p 5173:5173 -v "$(pwd):/app" -v /app/node_modules -e CHOKIDAR_USEPOLLING=true react-docker
🔧 Command Explanation:
🔹 docker run
This starts a new container from a specified image.

🔹 -p 5173:5173
This maps port 5173 from the container to port 5173 on your host machine.

Useful when running a development server like Vite, which defaults to port 5173.

You can open http://localhost:5173 in your browser.

🔹 -v "$(pwd):/app"
This bind mounts your current working directory ($(pwd)) to the /app directory inside the container.

This enables live reloading — any change you make to files locally is reflected immediately in the container.

/app is your app's working directory inside Docker.

🔹 -v /app/node_modules
This creates an anonymous volume for /app/node_modules inside the container.

Why? To prevent overwriting node_modules inside Docker with an (likely empty or incompatible) folder from your host system.

If you didn’t do this, mounting your project directory would also mount your (empty) host-side node_modules, breaking the app.

🔹 -e CHOKIDAR_USEPOLLING=true
This sets the environment variable CHOKIDAR_USEPOLLING=true inside the container.

This tells Chokidar (used by many dev tools like Vite, Webpack, etc.) to use polling instead of native file system watching.

Polling is slower but more reliable in Docker containers, where native file system notifications often don't work properly.