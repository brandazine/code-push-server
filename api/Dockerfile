FROM --platform=$BUILDPLATFORM node:18-alpine AS builder

WORKDIR /app

COPY . .

RUN npm install
RUN npm ci
RUN npm run build

FROM --platform=$TARGETPLATFORM node:18-alpine

WORKDIR /app

COPY --from=builder /app/dist ./dist
COPY --from=builder /app/package*.json ./

RUN npm ci --only=production && \
    npm cache clean --force

ENV NODE_ENV=production
ENV PORT=3000

ARG APP_BUILD_TIME
ENV APP_BUILD_TIME=${APP_BUILD_TIME}

ARG APP_COMMIT_SHA
ENV APP_COMMIT_SHA=${APP_COMMIT_SHA}

ARG APP_VERSION
ENV APP_VERSION=${APP_VERSION}

EXPOSE 3000

CMD [ "npm", "run", "start:env" ]