# Virtual Dev Env

## Introduction

Simple setup to easily create virtual development environment with vagrant and virtualbox. Vagrant tool allows you to easily create and manage virtual environment.
We are going to use virtualbox as provider for vagrant developer environment.

## Setup Virtualbox in Arch Linux

* Enter below command to update:

    ```sh
    sudo pacman -Syu
    ```

* Enter below command to install virtualbox:

    ```sh
    sudo pacman -S virtualbox
    ```
Pacman package manager should ask you which VirtualBox host module you want to install. Press 2 and then Enter to select the option virtualbox-host-modules-arch.

* Restart your computer.

* To enable virtualbox driver enter below command:

    ```sh
    sudo modprobe vboxdrv
    ```

* To automatically enable virtualbox driver. Use command:

    ```sh
    sudo nano /etc/modules-load.d/virtualbox.conf
    ```

Just type "vboxdrv" as shown in the screenshot below. Then save the file by pressing Ctrl+X and then press ‘y’ and then press Enter.

* Now you must add your Arch Linux login user to the ‘vboxusers’ system group. Doing so let’s a normal user use VirtualBox and all of its features. Otherwise you will see many restrictions when you run VirtualBox. Run the following command to add your login user to the ‘vboxusers’ group:

    ```sh
    sudo usermod -aG vboxusers YOUR_USER_NAME_HERE
    ```

* Now reboot your computer. Once your computer boots, run the following command to check whether vboxdrv kernel module was loaded automatically on system boot or not:

    ```sh
    sudo lsmod | grep vboxdrv
    ```

## Setup Vagrant in Arch Linux

* Install vagrant using below command:

    ```sh
    sudo pacman -S vagrant
    ```

* Now create your project directory and copy **Vagrantfile** into the directory. Create **data** folder inside your project directory which is used to sync data inside vagrant virtual machine. To create your own **Vagrantfile** use below command:

    ```sh
    vagrant init
    ```

* Enter below command to activate vagrant:

    ```sh
    vagrant up --provider=virtualbox
    ```
* Vagrant will download vagrant box **archlinux/archlinux** if it's not already available on your computer. For more vagrant box list [check this link](https://app.vagrantup.com/boxes/search).

* Once virtual box is running, use below command to connect using SSH:

    ```sh
    vagrant ssh
    ```

* Provided **Vagrantfile** setup **data** folder in project directory to sync inside vagrant. To access the shared folder you can change directory to **/vagrant_data**.

* To stop vagrant virtual machine use command:

    ```sh
    vagrant halt
    ```
* To suspend vagrant virtual machine use command:

    ```sh
    vagrant suspend
    ```

* To destory vagrant virtual machine use command:

    ```sh
    vagrant destroy
    ```
* The `destroy` command does not remove a box that may have been installed on your computer during `vagrant up`. Thus, even if you run `vagrant destroy`, the box installed in the system will still be present on the hard drive. To return your computer to the state as it was before `vagrant up` command, you need to use `vagrant box remove`.

## Special Tips

### Setup Java in Arch Linux

* To install JDK use commands:

    ```sh
    sudo pacman -Syu
    sudo pacman -S jar-openjdk
    sudo pacman -S jdk-openjdk
    ```
