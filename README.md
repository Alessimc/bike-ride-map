# Bike Rides Map

![Bike Rides Map](path/to/screenshot.png) <!-- Add a screenshot of your map here -->

This project displays an interactive map of all your bike rides, with routes automatically updated from Strava or Komoot. The map is designed to run in full-screen mode on a digital picture frame, creating a dynamic, visual art piece of your biking adventures.

## Features

- Interactive map with bike ride routes
- Automatic GPX file updates from Strava or Komoot
- Full-screen display suitable for digital picture frames

## Project Structure

```
bike-rides-map/
├── gpx/                # Directory to store GPX files
│   ├── ride1.gpx
│   ├── ride2.gpx
│   └── ...             # Additional GPX files
├── js/
│   └── update_gpx_files.py  # Python script to update the GPX list
├── data/
│   └── gpx_files.json  # JSON file listing all GPX files
├── index.html          # Main HTML file for the map
├── styles.css          # Optional custom styles for the map
└── README.md           # Project documentation
```

## Setup Instructions

### Prerequisites

- A digital picture frame or a Raspberry Pi connected to an HDMI display
- A web server (e.g., `nginx` or `Apache`)
- Python 3.x

### Installation

1. **Clone the repository**

```sh
git clone https://github.com/yourusername/bike-rides-map.git
cd bike-rides-map
```

2. **Set up the web server**

Install nginx (or your preferred web server) and place your project files in the web server's root directory.

```sh
sudo apt update
sudo apt install nginx
sudo cp -r * /var/www/html/
```

3. **Configure auto-start for full-screen mode (Raspberry Pi)**

Edit the autostart file to launch Chromium in kiosk mode
```sh
nano ~/.config/lxsession/LXDE-pi/autostart
```
Add these lines:
```sh
@lxpanel --profile LXDE-pi
@pcmanfm --desktop --profile LXDE-pi
@xscreensaver -no-splash
@chromium-browser --start-fullscreen --kiosk http://localhost
```

4. **Set up the GPX update script**

Edit the update_gpx_files.py script with your Strava or Komoot API credentials. Ensure the script is executable and set up a cron job to run it periodically

```sh
chmod +x js/update_gpx_files.py
crontab -e
```

Add this line to run the script daily at midnight:

```sh
0 0 * * * /usr/bin/python3 /path/to/your/update_gpx_files.py
```

## GPX Update Script

Here’s a brief overview of how the update_gpx_files.py script works:

- Authenticates with Strava or Komoot using OAuth2
- Fetches recent activities
- Downloads GPX files for each activity
- Updates gpx_files.json with the list of GPX files

## Milestones

- [ ] Set up the project structure
- [ ] Create the interactive map with Leaflet.js
- [ ] Implement GPX file fetching from Strava
- [ ] Implement GPX file fetching from Komoot
- [ ] Configure full-screen mode on a Raspberry Pi
- [ ] Automate GPX updates with a cron job
- [ ] Test the full setup on a digital picture frame
- [ ] Add additional customization and styling
- [ ] Make everything easily installable with a requirements.txt or so.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgements

- [Leaflet](https://leafletjs.com/) for the interactive maps
- [Leaflet-GPX](https://github.com/mpetazzoni/leaflet-gpx) for GPX track support
- [Strava API](https://developers.strava.com/) and [Komoot API](https://developer.komoot.com/) for activity data