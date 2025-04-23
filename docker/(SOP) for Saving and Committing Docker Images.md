
---

### **1. Save the Docker Image for SSL**
1. Use the `docker save` command to export the Docker image:
   ```bash
   docker save release.enlightcloud.com/360-containers/emagic-app:v8.4.1 | gzip > /release-enlightcloud-com_360-containers_emagic-app-v8-4-1.tar.gz
   ```
2. Verify the tar.gz file is created successfully in the specified location.

---

### **2. Save Docker Images Permanently**

#### **Step 1: Identify the Docker Container**
1. List all containers and filter by name or image using `docker ps`:
   ```bash
   docker ps -a | grep emagic
   ```
   Example output:
   ```
   b46a52d8ca59   release.enlightcloud.com/360-containers/emagic-app
   ```

#### **Step 2: Commit Changes to the Container**
1. Commit the changes to create a new image:
   ```bash
   docker commit b46a52d8ca59
   ```
   Example output:
   ```
   sha256:90d09e94e490459a9b75f9a5c033a0a00a34ce2ceb846bc7ff139669696ae4bb
   ```

#### **Step 3: Verify the Newly Created Image**
1. Check the list of Docker images:
   ```bash
   docker images | more
   ```
   Example output:
   ```
   <none>  <none>     90d09e94e490   47 seconds ago
   ```

#### **Step 4: Tag the New Image**
1. Tag the newly created image with the desired name and version:
   ```bash
   docker tag 90d09e94e490 release.enlightcloud.com/360-containers/emagic-app:v8.4.1
   ```

#### **Step 5: Verify the Tagged Image**
1. Filter images by name to confirm the tag was applied:
   ```bash
   docker images | grep emagic
   ```
   Example output:
   ```
   release.enlightcloud.com/360-containers/emagic-app   v8.4.1   90d09e94e490   2 minutes ago
   ```

---

### **3. Summary Commands**
- **Save Docker Image:**
  ```bash
  docker save release.enlightcloud.com/360-containers/emagic-app:v8.4.1 | gzip > /release-enlightcloud-com_360-containers_emagic-app-v8-4-1.tar.gz
  ```
- **Commit Changes:**
  ```bash
  docker commit <container-id>
  ```
- **Tag Image:**
  ```bash
  docker tag <image-id> <repository>:<tag>
  ```
- **Verify:**
  ```bash
  docker images | grep <name>
  ```

