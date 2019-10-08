🛠 Documentation Work in Progress 🛠  

## Error: watch src ENOSPC

Increase `inotify.max_user_watches` if build fails on Ubuntu with `Error: watch src ENOSPC`:

```bash
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p