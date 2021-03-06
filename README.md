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
* For using with Windows8.1 and later Hyper-V provider (you must enable this feature in Windows first). Use below command in admin command prompt:

    ```sh
    vagrant up --provider=hyperv
    ```

* **Fixing Error - Warning: Authentication Failure. Retrying...**

    Add below config to VagrantFile just below   ```config.vm.box = "archlinux/archlinux"```
    
    ```sh
    config.ssh.username = "vagrant"
    config.ssh.password = "vagrant"
    ```


* Vagrant will download vagrant box **archlinux/archlinux** if it's not already available on your computer. For more vagrant box list [check this link](https://app.vagrantup.com/boxes/search). Remember that archlinux box doesn't work with Windows Hyper-V. For Hyper-V boxes, [check this link](https://app.vagrantup.com/boxes/search?provider=hyperv).

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

### Running Angular in Vagrant with Port Forwarding

```sh
ng serve --open --host 0.0.0.0
```

### Exclude folders in sync

Update folder sync in command in Vagrantfile with below:

```sh
config.vm.synced_folder "./data", "/vagrant_data", type: "rsync", :mount_options => ["dmode=777", "fmode=666"], rsync__exclude: ['node_modules/']
```

### Remote file with Visual Studio Code

Start vagrant machine and run command and copy output.

```sh
vagrant ssh-config
```

Install VS Code Remote-SSH extension and press `Ctrl + Shift + P`. Search SSH and Select - Connect to Host. Select configure host and select a ssh config file.
In config file, paste about ssh output.

Again press `Ctrl + Shift + P` and Connect to Host with name default.
