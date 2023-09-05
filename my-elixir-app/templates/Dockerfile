# Use the official Elixir image as the base image
FROM elixir:1.12.2-alpine
WORKDIR /app
RUN apk update && \
    apk add --no-cache build-base nodejs npm postgresql-client
COPY mix.exs mix.lock ./
RUN mix do deps.get, deps.compile
COPY . .
ENV MIX_ENV=prod
RUN mix compile
RUN cd assets && npm install && npm run deploy && cd ..
RUN mix release
EXPOSE 4000
CMD ["_build/prod/rel/my_app/bin/my_app", "start"]

