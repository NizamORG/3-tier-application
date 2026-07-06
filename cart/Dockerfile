FROM node:20-alpine AS build
WORKDIR /app

COPY package.json ./
RUN npm install --omit=dev --ignore-scripts

FROM node:20-alpine AS runtime
ENV NODE_ENV=production \
    INSTANA_AUTO_PROFILE=true
WORKDIR /app

RUN addgroup -S app && adduser -S -G app app
COPY --from=build /app/node_modules ./node_modules
COPY package.json ./package.json
COPY server.js ./server.js

USER app
EXPOSE 8080
CMD ["node", "server.js"]

