### Stage 1: Build

FROM node:lts-alpine AS build

#### make the 'app' folder the current working directory
WORKDIR /usr/src/app

#### copy both 'package.json' and 'package-lock.json'
COPY package*.json ./

#### install dependencies (Clean Install)
RUN npm ci

#### install angular cli
RUN npm install -g @angular/cli

#### copy rest of files
COPY . .

### build the application
RUN ng build --configuration "production"

# Stage 2: Run

FROM nginx:alpine

# Copy the build output to nginx document root
COPY --from=build /usr/src/app/dist/payoneer/browser /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Optimized CMD for nginx
CMD ["nginx", "-g", "daemon off;"]