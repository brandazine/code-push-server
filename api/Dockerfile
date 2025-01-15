FROM --platform=$BUILDPLATFORM node:18-alpine AS builder
WORKDIR /api

ENV NODE_ENV=production
ENV PORT=3000

ARG APP_BUILD_TIME
ENV APP_BUILD_TIME=${APP_BUILD_TIME}

ARG APP_COMMIT_SHA
ENV APP_COMMIT_SHA=${APP_COMMIT_SHA}

ARG APP_VERSION
ENV APP_VERSION=${APP_VERSION}

COPY . .

RUN npm install
RUN npm run build

RUN npm cache clean --force

EXPOSE 3000

CMD [ "npm", "run", "start:env" ]