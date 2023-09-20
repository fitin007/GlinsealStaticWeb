FROM node:lts AS build
WORKDIR /app

# Copy package.json and pnpm-lock.yaml to the working directory
COPY package.json pnpm-lock.yaml ./

# Install PNPM and dependencies
RUN npm install -g pnpm
RUN pnpm install
COPY . .
# Build the Astro app
RUN pnpm run build

FROM nginx:alpine AS runtime
COPY nginx.conf /etc/nginx/nginx.conf
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 8080

