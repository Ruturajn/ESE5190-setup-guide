# Pico-SDK Setup Guide

Now that we have our [Basic Environment](https://github.com/Ruturajn/ese5190-2022-lab2-into-the-void-star/blob/main/Basic_Setup.md) set up, we can move
forward to cloning the `pico-sdk`, and `pico-examples` repository to our local machine. In this guide, we will be going over the procedure to install
the dependencies for the `pico-sdk`, and getting it completely setup on *WSL running Ubuntu*.

### Installing Required Packages
- Let's first as always update our system, before we proceed to installing an packages.
  ```
  $ sudo apt update && sudo apt upgrade
  ```
- Then, the dependencies can be installed using,
  ```
  $ sudo apt install build-essential cmake gcc-arm-none-eabi libnewlib-arm-none-eabi libstdc++-arm-none-eabi-newlib
  ```
  Note that the package `libstdc++-arm-none-eabi-newlib` is also required since, I am on Ubuntu (which is Debian based distribution, this package may or
  may not be required depending on which distribution you are working with). The following is a screenshot of how the output from this command might look,
  
  ![Screenshot 2022-10-10 113536](https://user-images.githubusercontent.com/56625259/194908994-da28d18d-cbed-4aac-bb86-aed6a77ea10b.png)


### Cloning the Repositories
- Firstly, you will need `git` on your machine for completing this step (which I guess you already have, but let's confirm anyway),
  ```
  $ sudo apt install git
  ```
  If the package is already installed, `apt` will let you know, that you have it.
- Now, let's clone the `pico-sdk`, and the `pico-examples` repositories, but before we do that, I am going to create a separate folder in my `home`
  directory. I like to keep my *GitHub* folders separate from my normal folders.
  ```
  $ cd ~
  $ mkdir ./Git-Repos
  $ cd ./Git-Repos
  ```
- Executing the few commands listed above, will create a new directory named `Git-Repos` in your `home` directory, and navigate into it. Now, we can proceed to
  cloning the repositories (as explained in the SDK getting started guide),
  ```
  $ cd ~/Git-Repos
  $ mkdir pico
  $ cd ./pico
  $ git clone -b master https://github.com/raspberrypi/pico-sdk.git
  $ cd ./pico-sdk
  $ git submodule update --init
  ```
  Now, let's go back up a directory and clone the `pico-examples` repository,
  ```
  $ cd ../
  $ git clone -b master https://github.com/raspberrypi/pico-examples.git
  ```
  If everything was executed without errors, you should see something like this as an output,
  
  ![Screenshot 2022-10-10 113510](https://user-images.githubusercontent.com/56625259/194909352-a54d8973-a385-49d5-94bd-a2f1c811acd4.png)

### Building Examples

As a sanity check, let's try building the examples from the `pico-examples` repository as described in the getting started guide.

- Navigate to the `pico-examples` folder (I assume you have set it up as described in the section above, if not your path may differ),
  
  ```
  $ cd ~/Git-Repos/
  ```
  Also, make sure that you have cloned both the `pico-sdk` and the `pico-examples` respositories in the same root directory. For example,
  the following is what my file tree looks like,
  ```
  .
  └── pico
      ├── pico-examples
      └── pico-sdk
  
  3 directories, 0 files
  ```
  Where, the `.` represents the current directory, which is `~/Git-Repos`. The above tree diagram can be extracted using the command,
  ```
  $ tree -L 2 .
  ```
  Here, `-L 2` asks the `tree` utility to only go two levels deep in the `.` (current) directory. Once you have confirmed this, we can move to the
  next step.
- Now, we need to create a `build` directory in our `pico-examples` folder and navigate into it,
  ```
  $ cd ./pico/pico-examples/ 
  $ mkdir build
  $ cd build
  ```
- The most important part is this, we need to set the `PATH` for our `pico-sdk` folder, which will be used during the build process (This step will not work if your
  directory structure is not right). To do this, if you are on a shell like `bash` or `zsh`,
  ```
  $ export PICO_SDK_PATH=../../pico-sdk
  ```
  To make this environment variable appear in everyone of your terminal sessions, just add a line to your `bashrc` or `zshrc`. Note that, the actual filesystem
  path will need to be changed. For example, in this case, the line should be something like (don't forget to change `<user_name>` with your actual *username*),
  ```
  $ export PICO_SDK_PATH=$PICO_SDK_PATH:/home/<user_name>/Git-Repos/pico/pico-sdk/
  ```
  If you are using something like the `fish` shell, the syntax is a bit different. Firstly, for the `$ export PICO_SDK_PATH=../../pico-sdk` command, the `fish`
  alternative is,
  ```
  $ set -gx PICO_SDK_PATH ../../pico-sdk
  ```
  For making this environment variable persist, add a line to your `config.fish` file. For example, in this case,
  ```
  $ set -gx PICO_SDK_PATH /home/<user_name>/Git-Repos/pico/pico-sdk/
  ```
- Great!, now we can build the examples with (make sure you are in the `build` directory that we created),
  ```
  $ cmake ../
  ```

If everything went well, you should see something like this on your terminal,

![Screenshot 2022-10-10 121256](https://user-images.githubusercontent.com/56625259/194913795-0d7f81f1-37a6-45aa-84b4-d0f8fca5a775.png)
