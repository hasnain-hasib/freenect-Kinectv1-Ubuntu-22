# Kinect Installation Guide for Ubuntu 22

This guide provides step-by-step instructions to set up Kinect on Ubuntu 22.

## Prerequisites

Make sure your system is up-to-date:

```bash
sudo apt-get update &&
sudo apt-get upgrade -y
```

## Installation Steps

1. Install necessary packages:

```bash
sudo apt-get install -y git-core cmake freeglut3-dev pkg-config build-essential libxmu-dev libxi-dev libusb-1.0-0-dev cython3 python3-dev python3-numpy
```

2. Clone the libfreenect repository:

```bash
git clone git://github.com/OpenKinect/libfreenect.git
```

3. Navigate to the libfreenect directory:

```bash
cd libfreenect
```

4. Create a build directory:

```bash
mkdir build && cd build
```

5. Run cmake:

```bash
cmake -L ..
```

6. Compile the code:

```bash
make
```

7. Install the compiled code:

```bash
sudo make install
```

8. Configure library paths:

```bash
sudo ldconfig /usr/local/lib64/
```

9. Add the current user to the `video` and `plugdev` groups:

```bash
sudo adduser $USER video
sudo adduser $USER plugdev
```

10. Configure udev rules for Kinect:

```bash
echo -e '# ATTR{product}=="Xbox NUI Motor"\nSUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02b0", MODE="0666"\n# ATTR{product}=="Xbox NUI Audio"\nSUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02ad", MODE="0666"\n# ATTR{product}=="Xbox NUI Camera"\nSUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02ae", MODE="0666"\n# ATTR{product}=="Xbox NUI Motor"\nSUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02c2", MODE="0666"\n# ATTR{product}=="Xbox NUI Motor"\nSUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02be", MODE="0666"\n# ATTR{product}=="Xbox NUI Motor"\nSUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02bf", MODE="0666"' | sudo tee /etc/udev/rules.d/51-kinect.rules
```

11. Navigate to the Python wrappers directory:

```bash
cd ~/libfreenect/wrappers/python
```

12. Clean and install the Python bindings:

```bash
sudo python3 setup.py clean
sudo python3 setup.py install
```

## Additional Steps (if the above method doesn't work)

1. Install Python 3 pip:

```bash
sudo apt install python3-pip
```

2. Edit the setup.py file:

```bash
nano ~/libfreenect/wrappers/python/setup.py
```

Find the lines containing references to `Cython.Compiler.Main.version` and `Cython.Compiler.Main.Version.version`. Replace them with `Cython.__version__`.

3. Clean and reinstall the Python bindings:

```bash
cd ~/libfreenect/wrappers/python
sudo python3 setup.py clean
sudo python3 setup.py install
```

---
