# pin-hwmon

Pins stable `/etc/hwmon` symlinks for CPU and GPU temperature sensors so paths don’t jump around between reboots (e.g., `/sys/class/hwmon/hwmonX`). Ships with a Waybar helper to display CPU temperature.

## What it does
- Detects sensors under `${HWMON_ROOT:-/sys}/class/hwmon`.
- CPU: matches `k10temp` or `zenpower`.
- GPU: matches `amdgpu` (optional).
- Selects temperature inputs by label priority:
  - CPU: `Tctl`, `Tdie`, `Composite` → else first `temp*_input`.
  - GPU: `Junction`/`junction`, `Edge`/`edge` → else first `temp*_input`.
- Creates symlinks:
  - `/etc/hwmon/cpu` → CPU device dir
  - `/etc/hwmon/cpu_tctl` → chosen CPU temp input
  - `/etc/hwmon/gpu` → GPU device dir (if present)
  - `/etc/hwmon/gpu_temp` → chosen GPU temp input (if present)
- Systemd oneshot service to apply on boot.
- Waybar helper `/usr/bin/cpu-temp-waybar` emitting JSON.

## Install (Arch/EndeavourOS)
```
makepkg -si
sudo systemctl enable --now pin-hwmon.service
```

## Waybar
Config snippet:
```json
{
  "custom/cpu_temp": {
    "exec": "/usr/bin/cpu-temp-waybar",
    "interval": 2,
    "return-type": "json"
  }
}
```

Style:
```css
#custom-cpu_temp.ok { color: #44d62c; }
#custom-cpu_temp.hot { color: #ffcc00; }
#custom-cpu_temp.critical { color: #ff1744; }
```

## Troubleshooting
- Ensure CPU sensor is present: `ls ${HWMON_ROOT:-/sys}/class/hwmon/*/name | xargs -I{} sh -c 'echo -n "{} -> "; cat {}'`
- AMD GPU: check `amdgpu` driver in use: `lspci -k | grep -A2 VGA`
- Mocking: set `HWMON_ROOT=/path/to/mock/sys` for testing without touching real `/sys`.

## Security
- Service runs as root to create symlinks under `/etc/hwmon`.
- Scripts are installed read-only.

## License
MIT