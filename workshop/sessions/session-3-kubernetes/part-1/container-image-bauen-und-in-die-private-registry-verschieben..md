# Container Image bauen und in die private Registry verschieben.

#### Build the container image

1. Define an environment variable named `MYPROJECT` set with the name of the application you generated in the previous section:

   ```bash
   export MYPROJECT=<your-app-name>
   ```

2. Change to the directory of the generated project.

   ```text
   cd $MYPROJECT
   ```

3. Ensure your local Docker engine is started.

   ```text
   docker ps
   ```

4. Build, tag \(`-t`\) and push the docker image to your container registry on IBM Cloud

   ```bash
   docker build -t $MYREGISTRY/$MYNAMESPACE/$MYPROJECT:v1.0.0 .
   docker push $MYREGISTRY/$MYNAMESPACE/$MYPROJECT:v1.0.0
   ```

