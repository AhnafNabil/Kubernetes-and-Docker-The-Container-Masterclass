# Starting and Managing Containers

In this demo, we will build on our previous session where we created the container `cc_busybox-A` but did not start it. We will demonstrate how to start, stop, restart, and rename containers using Docker commands.

## Starting a Container

Let's start the container `cc_busybox-A` which we created earlier.

### Steps:

1. **Start the Container:**
    - **Command**: `docker container start cc_busybox-A`
    - **Explanation**: This command starts the container named `cc_busybox-A`. We don't need to provide additional flags like `-itd` because they were already specified during the container's creation.

    ```sh
    docker container start cc_busybox-A
    ```

    - **Outcome**: The command will output the name of the container (`cc_busybox-A`) to confirm that it has started successfully.

2. **Verify Container Status:**
    - **Command**: `docker ps -a`
    - **Explanation**: This command lists all containers, including those that are running, stopped, or exited.

    ```sh
    docker ps -a
    ```

    - **Outcome**: The container `cc_busybox-A` should now be in the running state.

## Stopping a Container

Next, let's stop the container `cc_busybox_B`, which is currently running.

### Steps:

1. **Stop the Container:**
    - **Command**: `docker container stop cc_busybox_B`
    - **Explanation**: This command stops the container named `cc_busybox_B`.

    ```sh
    docker container stop cc_busybox_B
    ```

    - **Outcome**: The command will output the name of the container (`cc_busybox_B`) to confirm that it has stopped successfully.

2. **Verify Container Status:**
    - **Command**: `docker ps -a`
    - **Explanation**: This command lists all containers, including those that are running, stopped, or exited.

    ```sh
    docker ps -a
    ```

    - **Outcome**: The container `cc_busybox_B` will not appear in the list because we used the `--rm` flag during its creation. This flag automatically removes the container once it stops.

## Restarting a Container

Now, let's restart the container `cc_busybox-A`.

### Steps:

1. **Restart the Container:**
    - **Command**: `docker container restart -t 5 cc_busybox-A`
    - **Explanation**: This command restarts the container named `cc_busybox-A` and gives it a 5-second buffer time before restarting.

    ```sh
    docker container restart -t 5 cc_busybox-A
    ```

    - **Outcome**: The command will output the name of the container (`cc_busybox-A`) to confirm that it has restarted successfully.

2. **Verify Container Status:**
    - **Command**: `docker ps -a`
    - **Explanation**: This command lists all containers, including those that are running, stopped, or exited.

    ```sh
    docker ps -a
    ```

    - **Outcome**: The container `cc_busybox-A` should be up and running again.

## Renaming a Container

Finally, let's rename the container `cc_busybox-A` to something simpler.

### Steps:

1. **Rename the Container:**
    - **Command**: `docker container rename cc_busybox-A my-busybox`
    - **Explanation**: This command renames the container from `cc_busybox-A` to `my-busybox`.

    ```sh
    docker container rename cc_busybox-A my-busybox
    ```

    - **Outcome**: The command will successfully rename the container without restarting it.

2. **Verify Container Status:**
    - **Command**: `docker ps -a`
    - **Explanation**: This command lists all containers, including those that are running, stopped, or exited.

    ```sh
    docker ps -a
    ```

    - **Outcome**: The container will appear in the list with its new name `my-busybox`.

## Summary

In this session, we covered:

- **Starting a Container**:
    - Command: `docker container start <container_name>`
    - Example: `docker container start cc_busybox-A`

- **Stopping a Container**:
    - Command: `docker container stop <container_name>`
    - Example: `docker container stop cc_busybox_B`

- **Restarting a Container**:
    - Command: `docker container restart -t <time> <container_name>`
    - Example: `docker container restart -t 5 cc_busybox-A`

- **Renaming a Container**:
    - Command: `docker container rename <old_name> <new_name>`
    - Example: `docker container rename cc_busybox-A my-busybox`

By following these steps, you can manage the lifecycle of Docker containers effectively. In the next lecture, we will explore more application-related operations with our containers.