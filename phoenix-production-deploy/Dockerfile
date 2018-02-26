FROM elixir:1.6.1-alpine

# Environment Variables
ENV APP_NAME hello_world
ENV APP_DIR /app
ENV MIX_ENV prod
ENV PORT 4000

# Dependencies
RUN mix local.hex --force
RUN mix local.rebar --force
RUN apk add --update nodejs
RUN apk add bash

# Copy files
COPY . ${APP_DIR}
WORKDIR ${APP_DIR}

# Pull dependencies
RUN mix deps.get

# Follow 3 Build steps
# according to https://github.com/bitwalker/distillery/blob/master/docs/Use%20With%20Phoenix.md

# Step 1 build assets in production mode
WORKDIR ${APP_DIR}/assets
RUN npm install
RUN ./node_modules/brunch/bin/brunch b -p


# Step 2 compress assets and tags for caching
WORKDIR ${APP_DIR}
RUN mix phx.digest

# Step 3 Build an OTP release
RUN mix release

# Run server
EXPOSE 4000
CMD [ "_build/prod/rel/${APP_NAME}/bin/${APP_NAME}", "foreground" ]
