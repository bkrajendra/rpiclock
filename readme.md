# Raspberry Pi Digital Clock and Weather Display

This project turns a Raspberry Pi connected to an HDMI display into a simple always-on digital clock with live weather updates, built using HTML, CSS, and JavaScript.

---

## Features

- Large, easy-to-read digital clock.
- Live weather information (temperature & description) using OpenWeatherMap.
- Auto-refreshes time every second and weather every minute.
- Runs in full-screen (kiosk mode).
- Designed for 24/7 operation with screen blanking disabled.

---

## Requirements

- Raspberry Pi with Raspberry Pi OS (Desktop version).
- HDMI display.
- Internet connection (for weather updates).
- Chromium browser installed.
- OpenWeatherMap API key (free).

---

## Getting Started

1. **Clone this repository:**

   ```bash
   git clone https://github.com/bkrajendra/rpiclock.git
   cd rpiclock

2. **Install Chromium**
    ```
    sudo apt update
    sudo apt install chromium-browser --yes
    ```
3. **Edit/Create config.json**
  Replace YOUR_OPENWEATHERMAP_API_KEY with your actual API key and the City of choice.
    ```
    {
      "apiKey": "YOUR_OPENWEATHERMAP_API_KEY",
      "city": "Pune,in"
    }
    ```
4. **Autostart**

   Autostart rpiclock

    ```
    sudo nano /etc/systemd/system/rpiclock.service

    ```

    ```
    [Unit]
    Description=Simple Python HTTP Server for RPIClock Display
    After=network.target

    [Service]
    WorkingDirectory=/home/pi/clock
    ExecStart=/usr/bin/python -m http.server 8080
    Restart=always
    User=pi

    [Install]
    WantedBy=multi-user.target

    ```
    Enable service
    ```
    sudo systemctl daemon-reload
    sudo systemctl enable rpiclock.service
    sudo systemctl start rpiclock.service
    sudo systemctl status rpiclock.service

    ```

   Auto start chromium
    ```
    nano ~/.config/lxsession/LXDE-pi/autostart

    ```
    Add Following at the end

    ```
    @chromium-browser --noerrdialogs --disable-infobars --kiosk http://localhost:8080


    ```

5. **Disable Screen blanking**
    ```
    @xset s off
    @xset -dpms
    @xset s noblank


    sudo reboot

    ```



## License
This project is open-source and available under the MIT License.

## Credits
Made with ❤️ for Raspberry Pi by Rajendra.
Feel free to fork and improve!