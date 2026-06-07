# Option: node:20-alpine + Multi-stage + Non-root
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN --mount=type=cache,target=/root/.npm npm ci
COPY . .
RUN npm run build

FROM node:20-alpine AS runtime
RUN apk add --no-cache tini
RUN addgroup -S sre_group && adduser -S sre_user -G sre_group
WORKDIR /app
COPY --from=builder --chown=sre_user:sre_group /app/dist ./dist
COPY --from=builder --chown=sre_user:sre_group /app/node_modules ./node_modules
USER sre_user
EXPOSE 8080
ENTRYPOINT ["/sbin/tini","--"]
CMD ["node","dist/server.js"]