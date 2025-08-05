### Build & Run Instructions  

**Step 1:** Build the Spring Boot JAR
```bash
cd simple_JAVA_app
mvn clean package
```
Thiw will create the **output:** target/demo-0.0.1-SNAPSHOT.jar

**step 2 :**  Build the Docker Image

```bash
docker build -t springboot-docker-demo .
```
**step 3 :** Run the Docker Container
```bash
docker run -p 8080:8080 springboot-docker-demo
```

## Open your browser at:
http://localhost:8080

**Expected Output**
```bash
Hello from Spring Boot Docker!
```




