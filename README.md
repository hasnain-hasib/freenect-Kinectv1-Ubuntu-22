 basic commands to install libfreenect and run the Kinect v1 on Ubuntu:

### Installation:

1. **Install required dependencies**:

   ```bash
   sudo apt-get update
   sudo apt-get install git build-essential cmake libusb-1.0-0-dev freeglut3-dev
   ```

2. **Clone the libfreenect repository**:

   ```bash
   git clone https://github.com/OpenKinect/libfreenect.git
   ```

3. **Build and install libfreenect**:

   ```bash
   cd libfreenect
   mkdir build
   cd build
   cmake ..
   make
   sudo make install
   ```

### Running Kinect:

4. **Create a udev rule to grant permissions**:

   Create a file `/etc/udev/rules.d/51-kinect.rules` with the following content:

   ```
   SUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02ae", MODE="0666"
   ```

   This rule will allow all users to access the Kinect device.

5. **Reload udev rules**:

   ```bash
   sudo udevadm control --reload-rules && sudo udevadm trigger
   ```

6. **Plug in the Kinect and run `freenect-glview`**:

   ```bash
   freenect-glview
   ```

   This command should open a window displaying the Kinect's depth and RGB data.

 including the tilt angle, as needed for your specific application. Please note that running `freenect-glview` might require elevated privileges (`sudo`) if you haven't configured the udev rules and group memberships correctly.

