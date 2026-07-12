## What is Tailscale?

Tailscale is a VPN (Virtual Private Network) service based in the WireGuard protocol, which permits you to connect devices together safely, without the need of encrypting your data or paying for a subscription.
It can be used with the Home Assitant companion app on your phone to connect to it from anywhere in the world.

---

## How to Install it in Home Assistant

### Step 1: Install the Tailscale Add-on 
1. **Open the Add-on Store**  
   In the Home Assistant search tool, search for "Add-on store".
  
2. **Install the Tailscale add-on**  
  Click to install it, then enable Start on boot and Watchdog, then click Start.

<div align="center">
  <img src="https://cdn.discordapp.com/attachments/1005273511918579765/1525662097738829955/image.png?ex=6a54330d&is=6a52e18d&hm=7a5df9160abf0f5d67e7086d28822a84b9fb38713f313ececa470e76419696dc&" alt="Tailscale" width="600"/>
  <h3></h3>
</div>

---

### Step 2: Authenticate your Tailscale Account

1. **Open the Tailscale Tab**  
   After it has finished starting up, open the Tailscale tab on your Home Assitant Supervisor.

2. **Login with your Account**  
   Click on the **Login** button, then sign in with your account.

<div align="center">
  <img src="https://media.discordapp.net/attachments/1005273511918579765/1525662193159373012/image.png?ex=6a543324&is=6a52e1a4&hm=ef94540ce0bb6eced0f904a491be36fc400ca46bc420026eb0a26a27233fa841&=&format=webp&quality=lossless&width=1228&height=544" alt="Tailscale login" width="600"/>
  <h3></h3>
</div>

  Once you're done logging in, refresh the page. Your Home Assistant will now have an IP that should look like this
  ```
  100.x.x.x
  ```
3. **Allow Subnet Routes**  
  In the [Tailscale Admin Panel](https://login.tailscale.com/admin/machines), search for the Home Assistant device, click on the three-dot menu on the side and select **Review route settings**, then click to allow subnet routes.

<div align="center">
  <img src="https://cdn.discordapp.com/attachments/1005273511918579765/1525665153146683432/image.png?ex=6a5435e5&is=6a52e465&hm=0ac685b4dff4dd76e41a9073e176a6168c8a321c97e55be33c2c06a25fa3324e&" alt="Allow subnet routes" width="600"/>
  <h3></h3>
</div>

---

### Step 3: Download the Tailscale app in your Device

1. **Download Tailscale**  
   Download the Tailscale Client [here](https://tailscale.com/download), choosing the download type according to your device.

2. **Log on your account**  
   Log in the same account you log on Home Assistant.

3. **Activate the VPN**  
   Search for the VPN activation button, then click on it to initiate the connection.

<div align="center">
  <img src="https://cdn.discordapp.com/attachments/1005273511918579765/1525665771056009387/image.png?ex=6a543679&is=6a52e4f9&hm=e2cd187044f501dd58ac02ed4077953a0e068b1a2fe678e04a62e67fca0ea6c2&" alt="Activate VPN" width="300"/>
  <h3></h3>
</div>

---

### Step 4: Using the Supervisor Remotely

1. **Web Browser**  
   Use the IP assigned to your Home Assistant device in the Tailscale network, with the 8123 port:
   ```
   http://100.x.x.x:8123
   ```
2. **Phone App**  
   When assigning the link for using the Supervisor in the phone companion app, use the IP mentioned above.
