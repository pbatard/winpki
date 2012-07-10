AC_INIT([winpki], [0.0.1], [https://github.com/pbatard/winpki/issues], [winpki], [https://github.com/pbatard/winpki])
AM_INIT_AUTOMAKE([-Wno-portability foreign no-dist no-dependencies])
AC_CONFIG_SRCDIR([src/pki.c])
AC_CONFIG_MACRO_DIR([m4])
# Enable silent build rules by default (Automake v1.11 or later).
# Disable by either passing --disable-silent-rules to configure or passing V=1 to make
m4_ifdef([AM_SILENT_RULES], [AM_SILENT_RULES([yes])],
         [AC_SUBST([AM_DEFAULT_VERBOSITY], [1])])

AC_PREREQ([2.50])
AC_PROG_CC
AC_PROG_RANLIB
AC_PATH_PROG(RM, rm, rm)
AC_CHECK_TOOL(STRIP, strip, strip)
AC_CHECK_TOOL(WINDRES, windres, windres)
AC_C_INLINE
AC_DEFINE([_GNU_SOURCE], [], [Use GNU extensions])

# Clang needs an explicit WIN32_WINNT defined else it produces warnings
AM_CFLAGS="${AM_CFLAGS} -DWINVER=0x501 -D_WIN32_IE=0x501 -D_WIN32_WINNT=0x501"
AM_LDFLAGS="${AM_LDFLAGS} -Wl,-no-undefined"

# Debug symbols
AC_ARG_ENABLE([debug],
	[AS_HELP_STRING([--enable-debug],
		[keep debug symbols for gdb (default=yes)])],
	[debug_enabled=$enableval],
	[debug_enabled='yes'])
if test "x$debug_enabled" != "xno" ; then
  CFLAGS="-g -O2"
else
  CFLAGS="-O2"
  LDFLAGS="-s"
fi

# check for -Wno-pointer-sign compiler support (GCC >= 4)
saved_CFLAGS="${CFLAGS}"
CFLAGS="$CFLAGS -Wno-pointer-sign"
AC_COMPILE_IFELSE([AC_LANG_PROGRAM([])],
	[nopointersign_cflags="-Wno-pointer-sign"], [nopointersign_cflags=""])
CFLAGS="${saved_CFLAGS}"

AM_CFLAGS="$AM_CFLAGS -std=gnu99 -Wshadow -Wall -Wundef -Wunused -Wstrict-prototypes -Werror-implicit-function-declaration $nopointersign_cflags"

AC_SUBST([VISIBILITY_CFLAGS])
AC_SUBST([AM_CFLAGS])
AC_SUBST([AM_LDFLAGS])

AC_CONFIG_FILES([Makefile])
AC_CONFIG_FILES([src/Makefile])
AC_OUTPUT
