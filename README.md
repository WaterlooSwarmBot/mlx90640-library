# mlx90640-library

Fork of pimoroni's mlx940640 software, for use in the TurtleBot4

## Raspberry Pi Users

** EXPERIMENTAL **

This port uses either generic Linux I2C or the  bcm2835 library.
Upon building, the mode is set with the I2C_MODE property, i.e. `make I2C_MODE=LINUX` or `make I2C_MODE=RPI`. The default is LINUX, without the need for the bcm2835 library or root access.

### Generic Linux I2C Mode

Make sure the Linux I2C dev library is installed:

```text
sudo apt-get install libi2c-dev
```

To get the best out of your sensor you should modify `/boot/firmware/usercfg.txt` and change your I2C baudrate to 400 kHz:

```text
dtparam=i2c1=on,i2c1_baudrate=400000
```

Now build the MLX90640 library and examples in LINUX I2C mode:

```text
make clean
make I2C_MODE=LINUX
```



### Dependencies

On the TurtleBot4's, a few additional dependencies are needed:

gstreamer plugins for the `rawrgb` and network streaming example:

```text
sudo apt-get install libgstreamer1.0-0 gstreamer1.0-dev gstreamer1.0-tools gstreamer1.0-doc
sudo apt-get install gstreamer1.0-plugins-base gstreamer1.0-plugins-good
```

# Building

After installing the dependencies, you can build the library. Build-modes are:

* `make` or `make all`: build the library and all dependencies. Default is to use standard linux I2C-Drivers, specify Raspberry Pi driver with `make I2C_MODE=RPI`
* `make examples`: only build examples, see below
* `sudo make install`: install libraries and headers into `$PREFIX`, default is `/usr/local`

Afterwards you can run the examples or build the python binding, see readme in the subfolder.
If you built the examples or library using the native bcm2835 I2C-Driver, you need to run all applications and examples as root.
Hence, `sudo examples/<exampleame>` for one of the examples listed below, or without `sudo` when using the standard Linux driver.

# Examples
## fbuf

```
make examples/fbuf
sudo examples/fbuf
```

This example uses direct-to-framebuffer rendering and black-blue-green-yellow-red-purple-white false colouring.

If you have issues with the output image, set "`IMAGE_SCALE`" to a smaller number.

## interp

```
make examples/interp
sudo examples/interp
```

This example uses direct-to-framebuffer rendering and black-blue-green-yellow-red-purple-white false colouring.

It also has 2x bicubic resize filter.

If you have issues with the output image, set "`IMAGE_SCALE`" to a smaller number.

## test

```
make examples/test
sudo examples/test
```

This example draws out to the console using ANSI colours and the full block char.

To see the actual temperature values, change "`FMT_STRING`" from the block char to the float format.

## step

```
make examples/step
sudo examples/step
```

Attempt to run in step by step mode (experimental)

