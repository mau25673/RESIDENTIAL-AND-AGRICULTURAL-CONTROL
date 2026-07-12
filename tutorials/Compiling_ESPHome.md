# How to Compile ESPHome Manually

In the case you got a Raspberry Pi 3 or version with a similar/lower processing power and memory, compiling the ESPHome through it may be impossible, in which case you'll need to compile it with your computer. 

---

## Step 1: Download all Dependencies  

1. **Install Python**
   The download can be done [here.](https://www.python.org/downloads/) During the installation process, be sure to check the **Add python.exe to PATH** option.
   
3. **Install Git**  
   The download can be done [here.](https://git-scm.com/install/)
   
5. **Install ESPHome**  
   Open a new terminal and run the following command:
   ```bash
   pip install esphome
   ```

---

## Step 2: Compiling the .yaml File

1. **Download the .yaml**  
   Download the .yaml file found [here.](../1_ESP/esphomeTudo.yaml)

2. **Running the Compiling Process**  
   On a terminal, run the following command:
   ```bash
    esphome compile esphomeTudo.yaml
   ```
  > Note: be sure that you're in the same folder the .yaml file is in.
  This process can take a few minutes.

---

## Step 3: Uploading the Binary

1. **Open the ESPHome Web Dashboard**  
   Instead of using the Home Assistant Supervisor, you'll need to use the [ESPHome Web Dashboard](https://web.esphome.io/?dashboard_install). Open it and connect your device, with the USB data cable physically connected to the ESP32 microcontroller and your computer.

2. **Upload the firmware.factory.bin File**  
   In the folder the compiling process was done in, search for the firmware.factory.bin file, which you can find with the following path:
   ```
   .esphome/build/livingroom/.pioenvs/livingroom/firmware.factory.bin
   ```
> Note: be sure that you can see hidden files.
  Hold down the **Boot** button until it starts uploading the files, in which case you can release it.
