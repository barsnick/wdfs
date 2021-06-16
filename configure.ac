AC_INIT(wdfs, 1.4.2, [noedler@web.de])
AM_INIT_AUTOMAKE
AM_CONFIG_HEADER(src/config.h)

AC_CHECK_HEADERS([pthread.h])
# defines HAVE_STRNDUP if strndup() is available
AC_CHECK_FUNCS([strndup])

AC_PROG_CC

have_fuse3_library="no"
PKG_CHECK_MODULES([FUSE], [fuse3], [
    have_fuse3_library="yes"
], [
    PKG_CHECK_MODULES([FUSE], [fuse >= 2.5.0], [
        have_fuse3_library="no"
    ])
])

PKG_CHECK_MODULES([WDFS], [neon >= 0.24.7 glib-2.0])

CFLAGS="$CFLAGS $WDFS_CFLAGS $FUSE_CFLAGS -Wall -D_GNU_SOURCE -D_REENTRANT"
if test "$have_fuse3_library" = "yes"; then
    CFLAGS="$CFLAGS -D_FILE_OFFSET_BITS=64 -DFUSE_USE_VERSION=30"
else
    CFLAGS="$CFLAGS -DFUSE_USE_VERSION=25"
fi
LIBS="$WDFS_LIBS $FUSE_LIBS"

AC_CONFIG_FILES([Makefile src/Makefile])
AC_OUTPUT

# eof
