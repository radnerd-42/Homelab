I was very interested in setting up a certificate authority for my homelab, and found instructions from [StepCA](https://smallstep.com/blog/build-a-tiny-ca-with-raspberry-pi-yubikey/) to do so. I also wanted to learn more aobut MFA tokens, and found [Picokey](https://www.picokeys.com/). 
For a while I struggled to get a Picokey setup based on the [instructions](https://github.com/polhenarejos/pico-fido) they provided on Github. I tried using a Waveshare RP2350-One dev board in this process, and had to troubleshoot a bit to get it working.
This is how I got things working, starting with updates for the necessary Python libraries, the Pico-SDK, Picotool, and finally the Picokey build itself. 

```
# Necessary updates 

sudo apt-get update
sudo apt-get install -y cmake python3 build-essential gcc-arm-none-eabi libnewlib-arm-none-eabi libstdc++-arm-none-eabi-newlib binutils-arm-none-eabi git
cd ~

# Get the Pico-SDK, and update it

git clone https://github.com/raspberrypi/pico-sdk.git
cd pico-sdk
git submodule update --init --recursive
cd ~

# Get the Picotool, and ensure it matches the needed version

git clone https://github.com/raspberrypi/picotool.git
cd picotool
git checkout 2.3.0
mkdir build
cd build
cmake ..
make
sudo make install
picotool version # make sure it get v2.3.0
cd ~

# Get the Pico-Fido repo, update, and build the .uf2

git clone https://github.com/polhenarejos/pico-fido.git
cd pico-fido
git submodule update --init --recursive
mkdir -p build
cd build
PICO_SDK_PATH=<path to pico-sdk>
cmake .. -DPICO_BOARD=pico DUSB_VID=<VID for your use> -DUSB_PID=<PID for your use> # the IDs tell the software tools what your key is, you need to determine and identify what those IDs are.
make

# Your .uf2 should be in the build/ directory
```
Once you have your .uf2, load it onto your dev board. For the RP2350-One I used, press and hold the boot button (on the left with the USB plug held away from you), and plug it into your computer. It should load as a drive, and you can then copy the .uf2 onto. Eject, and plug it back in, and you are good to go.
