# oneDrone-dr

for drone
***

## Settings
### 1. Hardware
#### Crow-D
<details>
  <summary>Change /boot/config.txt file</summary>

```text
# For more options and information see
# http://rptl.io/configtxt
# Some settings may impact device functionality. See link above for details

# uncomment if you get no picture on HDMI for a default "safe" mode
#hdmi_safe=1

# uncomment this if your display has a black border of unused pixels visible
# and your display can output without overscan
#disable_overscan=1

# uncomment the following to adjust overscan. Use positive numbers if console
# goes off screen, and negative if there is too much border
#overscan_left=16
#overscan_right=16
#overscan_top=16
#overscan_bottom=16

# uncomment to force a console size. By default it will be display's size minus
# overscan.
#framebuffer_width=1280
#framebuffer_height=720

# uncomment if hdmi display is not detected and composite is being output
#hdmi_force_hotplug=1

# uncomment to force a specific HDMI mode (this will force VGA)
#hdmi_group=1
#hdmi_mode=31

# uncomment to force a HDMI mode rather than DVI. This can make audio work in
# DMT (computer monitor) modes
#hdmi_drive=2

# uncomment to increase signal to HDMI, if you have interference, blanking, or
# no display
#config_hdmi_boost=4

# uncomment for composite PAL
#sdtv_mode=2

#uncomment to overclock the arm. 700 MHz is the default.
#arm_freq=800

# Uncomment some or all of these to enable the optional hardware interfaces
dtparam=i2c_arm=on
#dtparam=i2s=on
dtparam=spi=on

# Uncomment this to enable infrared communication.
#dtoverlay=gpio-ir,gpio_pin=17
#dtoverlay=gpio-ir-tx,gpio_pin=18

# Additional overlays and parameters are documented /boot/overlays/README

# Enable audio (loads snd_bcm2835)
dtparam=audio=on

[pi4]
# Enable DRM VC4 V3D driver on top of the dispmanx display stack
dtoverlay=vc4-fkms-v3d
max_framebuffers=2

[all]
dtoverlay=vc4-fkms-v3d
dtoverlay=dwc2,dr_mode=host
start_x=1
gpu_mem=128
dtparam=i2c_vc=on
enable_uart=1

#dtoverlay=uartx

dtoverlay=uart0
dtoverlay=uart1
dtoverlay=uart2
dtoverlay=uart3
dtoverlay=uart4
dtoverlay=uart5

dtoverlay=spi1-1cs

dtoverlay=disable-bt

```
</details>

### 2. Software
#### 1. Mosquitto broker
- install mosquitto broker
```shell
  > sh install_MQTT-broker.sh
```
- edit config file
```shell
  > sudo nano /etc/mosquitto/conf.d/default.conf
```
- add code
```
listener 1883
protocol mqtt
listener 8883
protocol websockets
socket_domain ipv4
allow_anonymous true
```
- restart mosquitto service
```shell
> sudo service mosquitto restart
```

#### 2. Python library
- install
```shell
> pip3 install -r requirements.txt
```

#### 3. Node.JS package
- install
```shell
> npm install
```

## Prepare
### 1. drone_info.json
- create
```shell
> nano drone_info.json
```
- edit
```json
{
    "id": "Dione",
    "approval_gcs": "MUV",
    "host": "gcs.iotocean.org",
    "drone": "KETI_Drone",
    "gcs": "KETI_GCS",
    "system_id": 250
}
```

## Run
- default
```shell
> npm start
```
