

## Objective

This SOP outlines the steps to deploy a React application in a production environment using Nginx as a web server. It resolves the issue of a React app showing a 404 error when running on Nginx and ensures proper routing.

---

## **Prerequisites**

- A React application ready for production.
    
- Nginx installed on the target server.
    
- Docker installed (if using Docker for deployment).
    

---

## **Steps to Deploy the React App**

### **1. Modify **``** for Correct Homepage Routing**

Ensure that the `homepage` property in `package.json` is set to `"."` to avoid routing issues.

#### **Update **``

```json
{
    "name": "enlight360",
    "version": "1.0.0",
    "private": true,
    "homepage": ".",
    "dependencies": {
        "@emotion/cache": "^11.4.0",
        "@emotion/react": "^11.4.0"
    }
}
```

After updating `package.json`, rebuild the React app:

```bash
npm run build
```

---

### **2. Configure Nginx for Path Redirection**

Create a new Nginx configuration file (`default.conf`) with proper routing settings.

#### **Create/Edit **``

```nginx
server {
    listen 80;

    root /usr/share/nginx/html;
    index index.html;

    location = / {
        rewrite ^/$ /ipam/ break; # Redirect root URL to the React app directory
    }

    location /ipam {
        try_files $uri /$uri /ipam/index.html; # Load static React app
    }

    gzip on;
    gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;
    gzip_vary on;
}
```

Copy this configuration file to `/etc/nginx/conf.d/default.conf`.

---

### **3. Copy Build Files to Nginx HTML Directory**

After building the React app, copy the generated `build` directory to the appropriate Nginx directory.

```bash
cp -r build /usr/share/nginx/html/ipam
```

If using Docker, follow the next step to build and deploy using a Dockerfile.

---

### **4. Deploy Using Docker (Optional)**

For containerized deployment, use the following Dockerfile to build and run the React app with Nginx.

#### **Create/Edit **``

```dockerfile
# Stage 1: Build Stage
FROM node:14 AS build
LABEL org.opencontainers.image.authors="sandesh.pawar@esds.co.in"
WORKDIR /app
COPY package*.json ./
RUN npm install --legacy-peer-deps
COPY . .
ENV ESLINT_NO_DEV_ERRORS=true
RUN npm run build

# Stage 2: Production Stage
FROM nginx:1.21.0-alpine AS production
ENV NODE_ENV=production

# Copy built assets from builder and consider "ipam" as the React app build
COPY --from=build /app/build /usr/share/nginx/html/ipam

# Add custom Nginx configuration
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose the web server port
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
```

---

### **5. Build and Run Docker Container (If Using Docker)**

Run the following commands to build and deploy the container:

```bash
docker build -t react-nginx-app .
docker run -d -p 80:80 react-nginx-app
```

---

## **Verification**

1. Open a web browser and navigate to `http://<server-ip>/ipam`.
    
2. Check the network tab in the browser developer tools to ensure no 404 errors occur.
    
3. If using Docker, verify the running container:
    
    ```bash
    docker ps
    ```
    
4. Check Nginx logs for any issues:
    
    ```bash
    tail -f /var/log/nginx/access.log
    tail -f /var/log/nginx/error.log
    ```
    

---

## **Conclusion**

By following this SOP, you can successfully deploy a React application with Nginx in a production environment. This setup ensures that the app loads correctly and handles routes without 404 errors.


