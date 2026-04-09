# Stage 1: Build
FROM node:18-alpine AS builder
WORKDIR /app
# Copy package files
COPY package*.json ./
# Install dependencies using ci (clean install for consistent builds)
RUN npm install
# Copy source code and build
COPY . .
ARG REACT_APP_API_URL
ENV REACT_APP_API_URL=$REACT_APP_API_URL
RUN npm run build

# Stage 2: Production
FROM node:18-alpine
WORKDIR /app
# Install 'serve' globally
RUN npm install -g serve
# Copy the build output from the builder stage
COPY --from=builder /app/build ./build
# Expose the application port
EXPOSE 3000
# Serve the static files
CMD ["serve", "-s", "build", "-l", "3000"]