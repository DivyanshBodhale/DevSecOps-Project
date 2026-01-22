# =========================
# Stage 1: Build
# =========================
FROM node:21-alpine AS backend-builder

WORKDIR /app

# Copy only dependency files (cache optimization)
COPY package*.json ./

# Install dependencies
RUN npm ci

# Copy application source
COPY . .

# =========================
# Stage 2: Runtime
# =========================
FROM node:21-alpine

WORKDIR /app

# Set production environment
ENV NODE_ENV=production

# Copy built app from builder
COPY --from=backend-builder /app /app

# Expose backend port
EXPOSE 5000

# Run app
CMD ["npm", "start"]
