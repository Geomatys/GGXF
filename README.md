# GGXF reader and writer
Experimental support of _Gridded Geodetic data eXchange Format_ (GGXF) files.
This is a format currently in development at the Open Geospatial Consortium (OGC).
See [OGC GitHub repository](https://github.com/opengeospatial/CRS-Gridded-Geodetic-data-eXchange-Format)
for more information.

This repository hosts a Maven project in the Java language.
At the time of writing this `README` file, the GGXF group has not yet made a final choice on the "carrier" format.
But HDF5 seems a good candidate.
This project uses the HDF5 library in C language published by the HDF5 group.
Java Native Interface (JNI) are provided by the HDF5 group as well.

## Building
The HDF5 native library must be installed manually.
All other dependencies are downloaded by the Maven project.
To install the HDF5 library, [download source files](https://www.hdfgroup.org/downloads/hdf5/)
version 1.12.1 (other versions may work as well by replacing occurrences of "1.12.1" in this project)
and execute the following commands from the directory where HDF5 source files have been decompressed:

```shell
./configure --enable-java --disable-static
make
make check              # Run test suite. Can be skipped (this is long).
make install            # Destination is the `hdf5/lib` sub-directory.
make check-install      # Verify installation.
```

Make the JAR file available to Maven by running the following command:

```shell
mvn install:install-file -Dfile=hdf5/lib/jarhdf5-1.12.1.jar \
    -DgroupId=org.hdfgroup -DartifactId=hdf-java -Dversion=1.12.1 \
    -Dpackaging=jar -DgeneratePom=true
```

To build this GGXF project, run the following commands from the directory where this project has been cloned:

```shell
export LD_LIBRARY_PATH=<directory of `hdf5/lib` sub-directory.>
mvn package
```

## References
* [OGC GGXF project](https://github.com/opengeospatial/CRS-Gridded-Geodetic-data-eXchange-Format)
* [Deformation model](https://github.com/opengeospatial/CRS-Deformation-Models)
* [GGXF example](https://github.com/opengeospatial/CRS-Gridded-Geodetic-data-eXchange-Format/tree/master/examples/deformation)
* [Download HDF5](https://www.hdfgroup.org/downloads/hdf5/)
* [Build HDF5-Java](https://portal.hdfgroup.org/display/support/HDF-Java)
* [HDF5 support page](https://portal.hdfgroup.org/display/HDF5/HDF5)
* [Apache SIS](https://sis.apache.org/)
