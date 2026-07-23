## Day 53 - Resolve VolumeMounts Issue in Kubernetes

## Task Details:

We encountered an issue with our Nginx and PHP-FPM setup on the Kubernetes cluster this morning, which halted its functionality. Investigate and rectify the issue:

The pod name is `nginx-phpfpm` and configmap name is `nginx-config` Identify and fix the problem.  

Once resolved, copy `/home/thor/index.php` file from the `jump host` to the `nginx-container within the nginx document root. 

After this, you should be able to access the website using Website button on the top bar.  

## Steps:

1. Inspect the `nginx-phpfpm` pod
    ```
    kubectl describe pod nginx-phpfpm
    ```
    > Under the `nginx-container` mount specifications, the path for shared-files was incorrectly set to /usr/share/nginx/html, mismatching the /var/www/html path expected by the PHP container and the Nginx configuration.

2. Export the Current Configuration to a YAML file
    ```
    kubectl get pod nginx-phpfpm -o yaml > nginx-pod.yaml
    ```

3. Open the exported YAML file to modify the mount path:
    ```
    vi nginx-pod.yaml
    ```
    > Locate the `nginx-container` block and edit the mountPath for the shared-files volume is /var/www/html
    ```
    mountPath: /var/www/html
    ```

4. Delete the old, misconfigured pod
    ```
    kubectl delete pod nginx-phpfpm
    ```

5. Apply the corrected manifest to launch the new pod
    ```
    kubectl apply -f nginx-pod.yaml
    ```

6. Confirm that both containers are mounting the volume to the identical path:
    ```
    kubectl describe pod nginx-phpfpm
    ```

7. Copy `/home/thor/index.php` file from the `jump host` to the `nginx-container`
    ```
    kubectl cp /home/thor/index.php nginx-phpfpm:/var/www/html/index.php
    ```
