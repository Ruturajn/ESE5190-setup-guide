# Guide to Setting up WSL and Neovim

On a Windows machine, the *Windows Subsystem for Linux*, can give us a UNIX-like terminal
experience, so I will be setting that up, along with *Neovim* as my text editor. Neovim is
a modern, fast, and lightweight *vim* based text editor (can be configured with `vimscript` or
`lua`).

### WSL

- Navigate to `Turn Windows Features On or Off`, by searching for it, in the start bar.
- Enable the option `Windows Subsystem for Linux`, in that window.
- You will be prompted to reboot the system to apply the changes, accept it, and restart your computer.
- Run the command `wsl --install` for installing the latest version of *Ubuntu* (you can choose any distribution that suits
your needs, here I am going with *Ubuntu*).
- After that, you will be prompted to create a username and password, for your distribution.
- Once you have setup the username and password, update your system, using
```
$ sudo apt update && sudo apt upgrade
```
- For a sanity check, let's try doing the exercise of creating a `*.txt` file, and printing out it's
contents, as described in Lab-2 Prelab.
    - Let's create a directory named `test` in our `home` directory.
    - Navigate to your `home` directory with `$ cd ~`, where the character `~` describes your `home` directory.
    - Now, we will create the `test` directory using `$ mkdir ./test`.
    - We will navigate to that directory using `$ cd ./test`.
    - A `text` file can be created using `$ touch testing.txt`.
    - We can write `Hello!! World` to the text file with `$ echo "Hello!! World" > ./testing.txt`.
    - To view the contents of the file use the command, `$ cat ./testing.txt`. If all went well you should see,
    `Hello!! World` printed on your terminal.
    - Now, let's go back a directory, and remove the `test` directory, since we don't need it anymore.
    ```
    $ cd ../
    $ rm -r ./test
    ```
- We have now ensured that everything is working perfectly, let's move to installing our text editor.

### Neovim

- Before we proceed to install packages, let us install the `build-essential` package available in the official
Ubuntu's repository, to install as the name suggests all the packages that are essential for building and compiling
various software. This can be done by running the following command,
```
$ sudo apt install build-essential
```
- Once the installation completes, you will be able to access your prompt again, now we can proceed to install
*Neovim*. For this, we will be grabbing the latest release of neovim from its github repo, since the Ubuntu
repositories don't have the latest version. The steps for acheiving that are as follows ([link to the *Releases* page for neovim](https://github.com/neovim/neovim/releases)),
    - Grab the asset file named `nvim-linux64.deb`.
    - Download the file to your WSL with (get the link address to the file, by right cliking it, or you
        can directly download it using the windows GUI, which should ideally place the file under `C:/Users/<user_name>`/Downloads`.
        You can then navigate to that directory through WSL with `$ cd /mnt/c/<user_name>/Downloads`, if you choose the GUI option,
        ignore the command below),

        ```
        $ wget "https://github.com/neovim/neovim/releases/download/nightly/nvim-linux64.deb"
        ```
    - Now that we have the `.deb` file, we can install it using (make sure you are in the same directory as the `.deb` file),
        ```
        $ sudo apt install ./nvim-linux64.deb
        ```
    - Great!, `neovim` is now installed, you can access it by typing the command `nvim` in your terminal.
    - I use my nvim configuration located in my [Dotfiles](https://github.com/Ruturajn/Dotfiles/tree/main/nvim).


### PuTTY or MobaXterm

- Installing *PuTTY* is relatively very simple, you can just navigate to [PuTTY's Downloads Page](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html), and grab
    the `64-bit-msi` installer (assuming you are on a 64-bit system). Then just follow, the guided install, and PuTTY should be setup on your system.
- I already have *MobaXterm* setup on my system for accessing *Cadence* on *Biglab*, so I will be using the *PuTTY* built into that as my serial console. To get *MobaXterm*,
    you can check out the [Downloads](https://mobaxterm.mobatek.net/download.html) page, and install the *Free* version, by following the guided installer.


***This marks the end of our basic setup, going forward we will be using this for programming the RP2040.***
