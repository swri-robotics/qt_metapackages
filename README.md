Qt Metapackages
===============

This repository contains [ROS](http://www.ros.org/) [metapackages](http://wiki.ros.org/Metapackages)
that are useful for depending on the right version of Qt depending on which
distribution of ROS you are using.

Justification
-------------

[ROS Indigo](http://wiki.ros.org/indigo) and earlier use Qt 4, but 
[ROS Kinetic](http://wiki.ros.org/kinetic) and later on Ubuntu 16.04 and
later use Qt 5.  It is possible to write your CMakeLists.txt and C++ code in
such a way that they are compatible with both versions of Qt, the lack of
conditional dependencies in the 
[Catkin package.xml format](http://wiki.ros.org/catkin/package.xml) means
that you cannot have a single `package.xml` file that depends only on Qt 4
when building for ROS Indigo and Qt 5 when building for ROS Kinetic.  In some
cases, depending on [qt\_gui\_cpp](http://wiki.ros.org/qt_gui_cpp) is sufficient,
but that may include dependencies you do not want, and there are many Qt
libraries that it does not include.

This has lead to many packages with separate branches for Indigo and post-Indigo
development in which the only meaningful differences are in the `package.xml`
files, and keeping these branches synchronized is annoying and error-prone.

The metapackages provided by this repository depend on rosdep keys for each
platform that in turn depend on the appropriate Qt packages for that platform so
that your package can have a single branch that works for every ROS distribution.

Usage
-----

Just depend on the metapackage for the Qt library you want in your `package.xml`.
When running on Ubuntu 14.04 / ROS Indigo, it will transitively depend on the
equivalent Qt 4 package.  When running in Ubuntu 16.04 / ROS Kinetic or later,
it will transitively depend on the equivalent Qt 5 package.
