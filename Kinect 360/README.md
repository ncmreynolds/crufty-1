# Kinect 360

The Kinect 360 is a very cheap way to get an RGBD (RGB and depth) camera for a budget rover. These are poor performers compared to the latest depth cameras but they are usable.

## Hardware

Most Kinect 360 devices come with a proprietary lead which includes USB 2.0 and 12v power made specifically for connecting to the XBox 260. There was a PC connection kit made that breaks these out but these are uncommon and an unnecessary expense.

It is actually quite easy to cut the cable and splice on new connectors to make it usable as a generic USB device.

### Pinout

- Black - Ground
- Red - USB 5V
- White USB Data+
- Green USB Data-
- Brown 12v

Hacking cables or pair of sockets onto a shortened cable works very well. The camera will appear on the USB bus with only USB connected but will not function until supplied with 12v.

It is possible to strip the camera down, remove the tilt servo and make it run from 5V only but this is outside the scope of what I wanted to achieve.

## Software/drivers

Support for the Kinect 360 is done with the open source package [Open Kinect](https://openkinect.org/wiki/Main_Page), also known as libfreenect.

These instructions are based on but differ slightly from from those on the Open Kinect Wiki as those are generic and slightly out of date for the current state of the world. These are absolutely specific for Ubuntu 20.04 LTS as of 26/08/2022 and should work exactly.

There is a binary of libfreenect in the Ubuntu distribution but it misses some components and building the software isn't massively onerous so I would recommend this.

### Installation from source

First you will need to install the necessary software to build libfreenect from source.

```
sudo apt install -y cmake freeglut3-dev pkg-config build-essential libxmu-dev libxi-dev libusb-1.0-0-dev debhelper libudev-dev cmake-curses-gui
```

Then install and make libusb, which is a necessary part of building libfreenect.

```
git clone https://github.com/libusb/libusb
cd libusb
./autogen.sh
make
sudo make install
cd ..
```

Now you can clone and make libfreenect.

```
git clone https://github.com/OpenKinect/libfreenect
cd libfreenect
mkdir build
cd build
ccmake ..
```

This will start ccmake which is an interactive configuration for the make process. Check the following steps, you should not need to edit the include path but you should check it.

- Inside the ccmake editor, press c to configure
- Using the arrow keys, move to line with LIBUSB_1_INCLUDE_DIR
- **If necessary** press enter to edit the line, then change it to /usr/local/include/libusb-1.0
- Press enter when finished editing
- Press c to continue configuring
- If everything is correct, you will now get an option to press g to generate and exit

Now continue with the make process.

```
cmake ..
make
sudo make install
cd ..
```

The bulk of libfreenect is now installed but the system won't know where to find the shared libraries. Create a new file 'usr-local-libs.conf'.

```
nano usr-local-libs.conf
```

Add these two lines to it then exit with ctrl-x and say yes to saving the file.

```
/usr/local/lib64
/usr/local/lib
```

Move this new file into the correct location and activate the configuration.

```
sudo mv usr-local-libs.conf /etc/ld.so.conf.d/usr-local-libs.conf
sudo /sbin/ldconfig -v
```

You're almost there, the last step is to grab the firmware for the audio components of the Kinect from the Microsoft servers.

```
sudo python3 /usr/local/share/fwfetcher.py
cd..
```

### Installation from the Ubuntu repositories

This is much simpler than installing from source, simply use the following.

```
sudo apt install libfreenect
```

However audio will not work as this does not include the audio firmware, or the script to retrieve it.

### Enabling non-root use

TBC

### Testing the Kinect

Now all the libfreenect utilities should work, it is worth trying 'freenect-regtest' which will capture some .ppm image files, 'freenect-wavrecord' which will record some audio and  'freenect-tiltdemo' which will move the camera on its mount.

## Integration with ROS