## Software Installation and Configuration

### Step 1: Install Home Assistant on the Raspberry Pi
1. **Prepare the OS**  
   Use Raspberry Pi Imager to install *Home Assistant* on a MicroSD card.
2. **Boot the System**  
   Check to see if everything went smoothly, by either a monitor or following the next steps directly.

---

### Step 2: Open the Supervisor and Install ESPHome Add-on
1. **Connect the Raspberry Pi to the Internet**  
   This can be done either by connecting it directly by an ethernet cable or through Wi-Fi, through the following command:
   ```sh
   network update wlan0 --ipv4-method auto --ipv6-method auto --wifi-auth wpa-psk --wifi-mode infrastructure --wifi-ssid <Your_WiFi_SSID> --wifi-psk <Your_WiFi_Password>
   ```

2. **Open the Supervisor**  
   On a web browser connected to the same network as the Raspberry Pi, open the following URL:
   ```sh
   http://homeassistant.local:8123/
   ```
   It should take some time for it to finish booting up completely, so wait a few minutes after powering it before connecting to the supervisor.

3. **Create an User**  
   After succesfully opening the supervisor, a user must be created to be able to make use of the supervisor and control de Home Assistant supervisor.

4. **Install ESPHome Add-on**  
   In a computer connected to the same network as Home Assistant, open this link: https://my.home-assistant.io/redirect/supervisor_addon/?addon=5c53de3b_esphome&repository_url=https%3A%2F%2Fgithub.com%2Fesphome%2Fhome-assistant-addon  
   It will open a screen showing ESPHome add-on store's page, click on install, and check for it to open automatically.
   > Note: If you need more information to complete this step, it can be found in this guide: https://esphome.io/guides/getting_started_hassio/

---

### Step 3: Setting up ESPHome in the ESP32 microcontroller
1. **Creating a device**  
   Click on the "New Device" button in the bottom-right corner of the screen, where it will ask for Wi-Fi connection details before proceeding. Choose ESP32, then continue through the wizard to complete the installation. If this is the first time connecting the ESP32, you'll need a physical connection, which is where the micro-USB data cable will be used. Connect it to the ESP32, then click the three dot menu in the device you created and choose "Install", then choose install through direct connection with the supervisor computer.
   Before the upload process starts, press and hold the **Boot** button on the ESP32 microcontroller board, and keep it held down until ESPHome shows "Preparing installation", in which you can let go off the button.
   > Note: If you're using a Raspberry Pi with 1 GB of RAM, it won't be powerful enough to compile the .yaml file needed to configure the ESP32. You'll need to compile it in your own machine for it to work. A more in-depth tutorial can be found [here.](./tutorials/Compiling_ESPHome.md)

3. **Uploading the .yaml Code to the ESP32**
   You can find the .yaml code [here.](../1_ESP/esphomeTudo.yaml). Copy it and paste it onto the device .yaml, which you can do by clicking the Edit button on the bottom right corner of the device you just created:

<div align="center">
  <img src="https://media.discordapp.net/attachments/1005273511918579765/1525658824680149044/image.png?ex=6a543001&is=6a52de81&hm=ff2750f36465c8788c155ae0fca517ebb277047ff18c7898088c7361bde18374&=&format=webp&quality=lossless&width=337&height=96" alt="Edit button" width="600"/>
  <h3></h3>
</div>

   Now, go back to the three-dot menu and install it again, in which case it should now be working correctly. In the overview page, search for your living room, in which the configured sensors and pump should appear.
