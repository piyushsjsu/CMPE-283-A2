<h2 align="center">CMPE-283 Assignment 2 (Instrumentation via hypercall)</h2>

<b>Please refer screenshots folder to verify the completion of this assignment.</b>
<br/>
<br/>


<h4>Below are the steps for completing the assignment using GCP.</h4>

1. Create a VM Instance on GCP having atleast 8 cores and 32GB RAM (To make the builds faster) with nested virtualization enabled.

2. Run the below commands to install the required modules:
   * ```sudo apt-get install gcc```
   * ```sudo apt-get install make```
   * ```sudo apt-get install flex```
   * ```sudo apt-get install bison```
   * ```sudo apt-get install libssl-dev```
   * ```sudo apt-get install libelf-dev```
   * ```sudo apt-get install build-essential```
   * ```sudo apt-get install kernel-package```
   * ```sudo apt-get install ccache```
   * ```sudo apt-get install flex```
   
3. Fork (https://www.github.com/torvalds/linux) repo.

4. Clone the forked repo in your VM using the following command:
   * ```git clone https://github.com/<your_username>/linux.git```
   
5. Go to the cloned linux folder and copy the config of your VM's kernel to the current directory. Use the below command:
   * ```cp /boot/config-5.15.0-1025-gcp ~/linux/.config```

6. Build the kernel from the config we just copied. Run the following commands:
   * Build the kernel using the already existing config file
      * ```make oldconfig```
   * Prepare the linux
      * ```make prepare```
   * Build the modules
      * ```make -j <num_of_available_cores> modules```
   * Build the kernel itself
      * ```make -j <num_of_available_cores>```
   * Packaging the modules
      * ```sudo make INSTALL_MOD_STRIP=1 modules_install```
   * Install full built kernel to the VM
      * ```sudo make -j <your-vm-cpu-total-core-number> install``` 
   * Reboot to see changes
      * ```sudo reboot```
      
7. Run the below command to check if our kernel is installed:
   * ```uname -a```

8. To make changes in the kvm hypervisor, navigate to 'arch' directory:    
   * ```cd ~/linux/arch/x86/kvm```
 
9. Replace or modify vmx.c and cpuid.c files with the files present in this repo.

10. Go back to the top level of linux and perform Step 6.

11. Create an VM inside our current VM (nested VM). Install  virtual manager first using the below command:
    * ```sudo apt-get install virt-manager```
    
12. I tried to interact with the inner VM using the CLI but failed. I ended up using chrome desktop server.
    * https://cloud.google.com/architecture/chrome-desktop-remote-on-compute-engine
    
13. Go to https://remotedesktop.google.com/headless and follow the steps to connect to your inner VM instance.

14. Download ubuntu image using the following command:
    * ```wget https://releases.ubuntu.com/jammy/ubuntu-22.04.1-desktop-amd64.iso```

15. Open virt manager and install this ubuntu image on your inner VM using the GUI.
    * ```sudo virt-manager```
 
16. Now we can perform Assignment 2 on the inner VM. Create or copy test.c file from this repo on to you inner VM.

17. Compile and run test.c to verify the result.
   

