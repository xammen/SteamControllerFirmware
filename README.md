# steam controller firmware notes

sources:
- `SteamController` usbpcap capture
- `OldSteamController` usbpcap capture
- `punk` usbpcap capture (puck / dongle)

files:
- `firmware/steam_controller_firmware.bin`
  - size: 348032
  - sha256: `239D2EC43E20DAB7986F001CDD6F3C0496474DD30BC5A0575615BA4873AC493F`
  - build: beta from 2026-05-18
- `firmware/old_steam_controller_firmware.bin`
  - size: 347732
  - sha256: `69697A507D32657BDB47416DDD4FEAB64399155CE3F95AB52E09AA555CD5DC41`
  - build: firmware from 2026-05-12
- `firmware/steam_controller_puck_firmware.bin`
  - size: 195987
  - sha256: `CBA7E1800357633C99F28D5A2BACAF8587ED83F59BCD17FFCD5ACB0AD76AB4B2`

quick read:
- both steam controller builds are raw arm/thumb images for `nrf52833`
- same reset handler: `0x00025B15`
- same image shape, but not the same build
- new build uses zephyr `v3.7.99-b942d6a9f9f8`
- old build uses zephyr `v3.7.99-0f787cf982ce`
- the clearest added string in the new build is: `Failed to set stop on WTM`

what this looks like:
- mostly a small firmware update around imu / fifo watermark / sensor fusion handling
- no strong evidence here that it changes the controller mapping layer itself

notes:
- the update payload in the capture is framed with `ad 35 12` and byte-stuffed with `ac`
- the repo keeps the decoded binaries only, not the full usbpcap traces
