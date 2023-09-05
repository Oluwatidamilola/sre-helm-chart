# Use the official Elixir image as the base image
FROM elixir:1.12.2-alpine

# Set the working directory inside the container
WORKDIR /app

# Install system dependencies
RUN apk update && \
    apk add --no-cache build-base nodejs npm postgresql-client

# Copy mix.exs and mix.lock to the container
COPY mix.exs mix.lock ./

# Install and compile project dependencies
RUN mix do deps.get, deps.compile

# Copy the rest of the application code
COPY . .

# Set environment variables
ENV MIX_ENV=prod

# Compile the application
RUN mix compile

# Compile assets
RUN cd assets && npm install && npm run deploy && cd ..

# Build the release
RUN mix release

# Expose the necessary port for the Phoenix app
EXPOSE 4000

# Set the entrypoint for the release
CMD ["_build/prod/rel/my_app/bin/my_app", "start"]

