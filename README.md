# pin-hwmon

A small Arch Linux package that pins hwmon paths for stable CPU and GPU temperature access. This solves the issue where `/sys/class/hwmon/hwmonX` paths change across reboots, making it unreliable for scripts and monitoring tools.

## What it does

- Scans `/sys/class/hwmon` for CPU (k10temp/zenpower) and GPU (amdgpu) sensors.
- Creates stable symlinks under `/etc/hwmon`:
  - `/etc/hwmon/cpu` -> CPU hwmon directory
  - `/etc/hwmon/cpu_tctl` -> CPU temperature input (prefers Tctl, Tdie, Composite labels)
  - `/etc/hwmon/gpu` -> GPU hwmon directory (if present)
  - `/etc/hwmon/gpu_temp` -> GPU temperature input (prefers Junction, Edge labels)
- Provides a systemd oneshot service to run on boot.
- Includes a Waybar helper script for displaying CPU temperature.

## Installation

### From local source

```bash
git clone https://github.com/user/pin-hwmon.git
cd pin-hwmon
makepkg -si
sudo systemctl enable --now pin-hwmon.service
```

### Test the installation

```bash
# Check symlinks
ls -l /etc/hwmon

# Read CPU temperature
cat /etc/hwmon/cpu_tctl
awk '{printf "%.1f°C\n", $1/1000}' /etc/hwmon/cpu_tctl
```

## Waybar Integration

Add this to your Waybar config:

```json
{
  "custom/cpu_temp": {
    "exec": "/usr/bin/cpu-temp-waybar",
    "interval": 2,
    "return-type": "json"
  }
}
```

And style with CSS:

```css
#custom-cpu_temp.ok { color: #00ff00; }
#custom-cpu_temp.hot { color: #ffff00; }
#custom-cpu_temp.critical { color: #ff0000; }
```

## Troubleshooting

### No CPU sensor found
- Ensure the k10temp module is loaded: `sudo modprobe k10temp`
- Check available hwmon: `ls /sys/class/hwmon/`

### AMD GPU missing
- Ensure amdgpu drivers are in use: `lspci -k | grep amdgpu`
- Check if hwmon is exposed: `find /sys/class/hwmon -name name -exec cat {} \;`

### Show current mapping
```bash
ls -l /etc/hwmon
cat /etc/hwmon/cpu_tctl
```

## Acceptance Tests

After installation and enabling the service:

```bash
# Symlink exists
test -L /etc/hwmon/cpu_tctl

# Has content
[[ $(cat /etc/hwmon/cpu_tctl | wc -c) -gt 0 ]]

# Waybar script works
/usr/bin/cpu-temp-waybar
# Should print valid JSON and exit 0
```

## Security/Notes

- Scripts are installed read-only.
- Service is oneshot and runs with root privileges to create symlinks.
- No external dependencies beyond specified in PKGBUILD.

## License

MIT
