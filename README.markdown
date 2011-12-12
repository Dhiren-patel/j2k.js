
j2k.js
======

This is a port of OpenJPEG, an open-source JPEG2000 codec, to JavaScript using Emscripten.

Why? JPEG2000 is useful sometimes, and web browsers don't have native support for it, so having
a pure JS decoder is a nice option to have.


Usage
-----

Grab openjpeg.js which is an optimized and minified build. Then you simply call

```
    openjpeg(data, suffix)
```
with the first argument being an array of values in 0-255 (representing a file in binary format),
and the second argument being the suffix of the file (there is no autodetection of the file type
in OpenJPEG, and whether it is a .jp2 or .j2k does actually matter it turns out). The function
returns a a JSON object of form

```
    {
      width: the width
      height: the height
      data: the pixel data (in 24-bit "Planar RGB" format)
    }
```

See test.js for a concrete example (it is called by test.py).


Building
--------

(You don't normally need to do this.)

Do

```
    python make.py
```

Looks like you need |make clean| in build/ as incremental builds do not always link.

Testing
-------

Run

```
    python test.py openjpeg.js
```

The generated files are written to generated.raw. You can view them in GIMP
by opening them as RAW (select "all files", then "select file type" as raw,
and pick "generated.raw"). You should select "Planar RGB" as the format, and
enter the right width and height.

