#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ(2.59)
AC_INIT([dfu-util-multi],[0.7],[https://github.com/benlye/dfu-util-multi],,[https://github.com/benlye/dfu-util-multi])
AC_CONFIG_AUX_DIR(m4)
AM_INIT_AUTOMAKE([foreign])
AM_CONFIG_HEADER([config.h])

# Test for new silent rules and enable only if they are available
m4_ifdef([AM_SILENT_RULES], [AM_SILENT_RULES([yes])])

AM_MAINTAINER_MODE

# Checks for programs.
AC_PROG_CC

# Checks for libraries.
# On FreeBSD the libusb-1.0 is called libusb and resides in system location
AC_CHECK_LIB([usb], [libusb_init],, [native_libusb=no],)
AS_IF([test x$native_libusb = xno], [
    PKG_CHECK_MODULES([USB], [libusb-1.0 >= 1.0.0],,
        AC_MSG_ERROR([*** Required libusb-1.0 >= 1.0.0 not installed ***]))
])
AC_CHECK_LIB([usbpath],[usb_path2devnum],,,-lusb)

LIBS="$LIBS $USB_LIBS"
CFLAGS="$CFLAGS $USB_CFLAGS"

# Checks for header files.
AC_HEADER_STDC
AC_CHECK_HEADERS([usbpath.h windows.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST
AC_TYPE_SIZE_T

# Checks for library functions.
AC_FUNC_MEMCMP
AC_CHECK_FUNCS([ftruncate getpagesize usleep])

AC_CONFIG_FILES(Makefile src/Makefile doc/Makefile)
AC_OUTPUT
