# Lab 01

1. Create a new Pod named `nginx` running the image `nginx:1.17.10`. Expose container to port `80`. 

> Consider the two types of approaches: Imperative or Declerative.

2. Get the details of the Pod, including its IP address.

> Use kubectl -h for guidance. 

3. Create a temporary Pod that uses the busybox image to execute a `wget` command inside of the container. The `wget` command should access the endpoint exposed by the `nginx` container.


4. Get the logs of the `nginx` container.

5. Add the environment variables `DB_URL=postgressql://mydb:5432` and `DB_USERNAME=admin` to the container of the `nginx` Pod. 


6. Open a shell for the `nginx` container and inspect the contents of the currently directory `ls -l`.


7. Create a YAML manifest for a Pod named `loop` that runs the `busybox` image in a container. The container should run the following command: `for i in (1...10); do echo "Welcome $i times"; done`. Create the pod from the YAML manifest. What's the status of the Pod?


8. Edit the Pod named `loop`. Change the command to run in an endless loop. Each iteration should `echo` the current date. 

9. Inspect the events and the status of the Pod `loop`.

10. Delete the namespace `ckad` and its Pods. 


