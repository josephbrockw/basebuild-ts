# --- dev stage ---
FROM node:20-alpine AS dev
WORKDIR /app

# Faster installs with pnpm (corepack is preinstalled on Node 20)
RUN corepack enable && corepack prepare pnpm@9.11.0 --activate

# Install OS deps needed by Prisma
RUN apk add --no-cache openssl

# Copy only package files first for better layer caching
COPY package.json pnpm-lock.yaml* ./
# If you have a Nest-only package.json, keep it. If you inherited a root lockfile, it’s fine.

# Install deps
RUN pnpm install

# Copy source
COPY . .

# Generate Prisma client if using Prisma
# (Assumes prisma/schema.prisma exists in this app)
RUN pnpm prisma generate || true

EXPOSE 3001
CMD ["pnpm","start:dev"]
