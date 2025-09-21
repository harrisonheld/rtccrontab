# rtccrontab
`rtccrontab` is a lightweight cron replacement with automatic system wake-up support. It allows you to schedule tasks in a familiar crontab format while automatically setting your computer to wake up shortly before each job.

## How it works
- Stores user crontabs in `~/rtccrontab/rtccrontab`, completely separate from the system crontab.
- Uses standard cron syntax: `MIN HOUR DOM MON DOW COMMAND`.
- Generates a wrapper script for each job that:
  - Runs the command
  - Schedules `rtcwake` to wake the system 10 minutes before the next the next execution time.
- Installs a system cron file under `/etc/cron.d/rtccrontab-$USER` to execute the wrapper scripts at the scheduled times.

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