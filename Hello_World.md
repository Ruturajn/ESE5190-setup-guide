# Guide to the Hello World Example for RP2040

We now have our `pico-sdk` along with the environment setup. So, let's move on to the `hello_world` project, and get started.

### Building the Hello World Example

- Firstly, we navigate to the `build` directory in the `pico-examples` folder.
  ```
  $ cd ~/Git-Repos
  $ cd ./pico/pico-examples/build
  ```
- From here, we can go to the `hello_world` directory and build the project to create the `.uf2` binary (for this step make sure you have used
  `cmake` to generate the `Makefiles`, which is described in the sdk setup),
  ```
  $ cd ./hello_world
  $ make -j4
  ```
  The output should look something like this,
  
  ![Screenshot 2022-10-10 185142](https://user-images.githubusercontent.com/56625259/194968695-79ab54f3-d2bf-49c1-847b-e9d2c074f7a0.png)
  
  At the end, a successful build output is as follows,
  
  ![Screenshot 2022-10-10 185213](https://user-images.githubusercontent.com/56625259/194968720-f22c2cb9-7b0d-4b4e-98a2-09444e1c4346.png)
  
  Note that the `-j` flag passed to `make`, helps us assign the number of cores on which the build process should take place parallely.

- This step will generate build files. Among them binary named `hello_usb.uf2` needs to be placed in the RP2040, for it to be run. To do
  this, firstly we will hold down the `BOOTSEL` button, once the board is plugged in to the host computer. Now, press and release the `RST`
  button, which makes the RP2040 pop up as a USB mass storage.
- After this, drag and drop the `hello_usb.uf2` binary into the RP2040 (USB mass storage). Once, this is done the RP2040, will reboot
  umounting itslef, and the code will start executing.
- To view the output, we will access our serial console. For that, we need to figure out on which `COM` port is our board connected to
  (use *Device Manager*). In my case it is connected to `COM4`,
  
  ![Screenshot 2022-10-10 194349](https://user-images.githubusercontent.com/56625259/194970507-c825dac5-54cd-47ea-83e3-c5eb769efb67.png)

- I am using `MobaXterm`, which has `PuTTY` inbuilt as my serial console. Here, we start a new *Serial* session and choose our COM port
  along with the baud rate for the RP2040,
  
  ![Screenshot 2022-10-10 194433](https://user-images.githubusercontent.com/56625259/194970711-15c94aef-70b8-47f6-a8bf-8a230d31f435.png)

- If all went well, you will see `Hello, world!` printed onto your serial console,

  ![Screenshot 2022-10-10 190455](https://user-images.githubusercontent.com/56625259/194970969-9cee78d9-9d07-4ecd-874a-d66427f4bb43.png)

***Congrats!! you have now successfully cross-compiled and run your first C program on the RP2040.***
