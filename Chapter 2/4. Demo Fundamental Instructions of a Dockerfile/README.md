# Creating Your First Dockerfile: Step-by-Step Guide

In this guide, we will create our first Dockerfile and explore its fundamental instructions. The Dockerfile is an essential component for defining how a Docker image is built. Follow these steps to get started:

## Step 1: Verify Current Directory

First, verify your current working directory. If we are in a user directory, such as `/home/dhwani`, we should navigate to the provided `CC_Docker` directory after downloading and unzipping the course material.

```sh
pwd
```

## Step 2: Navigate to the `CC_Docker` Directory

Use the `ls` command to list the contents and ensure the `CC_Docker` directory is present. Then, navigate to it.

```sh
ls
cd CC_Docker
```

## Step 3: Navigate to the Module Directory

The `CC_Docker` directory contains subdirectories for each module. Navigate to the `S2` directory, which contains the necessary files for this segment.

```sh
cd S2
```

## Step 4: Navigate to the Demo Directory

Within `S2`, navigate to the `D-1` directory. This directory contains a pre-written Dockerfile for the demo, but we will create a new one to understand the process.

```sh
cd D-1
```

## Step 5: Create an Empty Dockerfile

Create an empty Dockerfile using the `touch` command.

```sh
touch Dockerfile
```

## Step 6: Open and Edit the Dockerfile

Open the Dockerfile using a text editor such as `nano`. You can use any text editor you prefer.

```sh
nano Dockerfile
```

## Step 7: Write the Dockerfile

Start writing the Dockerfile with fundamental instructions:

1. **ARG Instruction:**
   The `ARG` instruction defines a variable that users can pass at build-time to the builder with the `docker build` command. This helps keep parameters like versions under control.

    ```Dockerfile
    ARG CODE_VERSION=16.04
    ```

2. **FROM Instruction:**
   The `FROM` instruction sets the base image for subsequent instructions. It is essential in every Dockerfile and typically follows the `ARG` instruction if one is used.

    ```Dockerfile
    FROM ubuntu:${CODE_VERSION}
    ```

3. **RUN and CMD Instructions:**
   We include basic `RUN` and `CMD` instructions to add functionality, although their detailed exploration will come later.

    ```Dockerfile
    RUN apt-get update -y
    CMD ["bash"]
    ```

## Example Dockerfile

Here is the complete Dockerfile:

```Dockerfile
ARG CODE_VERSION=16.04
FROM ubuntu:${CODE_VERSION}
RUN apt-get update -y
CMD ["bash"]
```

## Step 8: Save and Exit

Save the file and exit the text editor. In `nano`, we can do this by pressing `CTRL + O` to save and `CTRL + X` to exit.

## Step 9: Build the Docker Image

Use the `docker build` command to build the Dockerfile into an image. The `-t` option tags the image with a name for easy reference.

```sh
docker build -t img_from .
```

## Step 10: Verify the Image

Verify that the image has been created using the `docker images` command. This command lists all Docker images on our system.

```sh
docker images
```

We should see the newly created `img_from` image listed among other Docker images.

## Summary

- **ARG Instruction:** Defines build-time variables.
- **FROM Instruction:** Sets the base image.
- **RUN and CMD Instructions:** Add functionality to the image.

By following these steps, we have created a simple Dockerfile, built a Docker image, and verified its creation. In the next sections, we will delve deeper into the `RUN` and `CMD` instructions and explore their uses in Dockerfiles.