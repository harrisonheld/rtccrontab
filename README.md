# rtccrontab
`rtccrontab` is a lightweight cron-like scheduler with automatic RTC wake-up support.  
It lets you define jobs in a familiar crontab format, and ensures your system wakes up a few minutes before each job runs.

## How it works
- Stores user jobs in `~/.rtccrontab/rtccrontab`, separate from the system crontab.
- Uses standard cron syntax: `MIN HOUR DOM MON DOW COMMAND`.
- Generates a wrapper script for each job that:
  - Runs the command
  - Calls `rtccrontab -w` to schedule the system to wake up for the next job.
- Installs a system cron file under `/etc/cron.d/rtccrontab-$USER` to execute the wrapper scripts at the scheduled times.
- Global config is read from `/etc/rtccrontab.conf`

## Usage
```bash
# Edit your rtccrontab
rtccrontab -e

# List your rtccrontab entries
rtccrontab -l

# Remove all rtccrontab jobs
rtccrontab -r
```

# Building the Debian Package
In the root directory, run:
```bash
dpkg-deb --build . rtccrontab.deb
```

# Installing
```bash
sudo dpkg -i rtccrontab.deb
```