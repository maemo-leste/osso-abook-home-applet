AC_INIT([osso-abook-home-applet], [4.3.0])
AC_CONFIG_MACRO_DIRS([m4])

AM_INIT_AUTOMAKE
AM_CONFIG_HEADER(config.h)

AC_PROG_CC
AM_PROG_CC_STDC
AM_PROG_CC_C_O
AC_PROG_INSTALL
AC_PROG_LIBTOOL

AM_GCONF_SOURCE_2
AC_PATH_PROG(GCONFTOOL, gconftool-2)

PKG_PROG_PKG_CONFIG([0.28])

PKG_CHECK_MODULES(
	APPLET,
	libhildondesktop-1
	gconf-2.0
	libosso-abook-1.0
	hildon-1
	dbus-1)

AC_ARG_ENABLE(debug,        [  --enable-debug           compile with DEBUG],,enable_debug=no)

if test "x$enable_debug" = "xyes"; then
	DEBUG_FLAGS="-DDEBUG"
fi

AC_ARG_ENABLE(cast-checks,      [  --disable-cast-checks         compile with GLIB cast checks disabled],[cchecks=${enableval}],cchecks=yes)
if test "x$cchecks" = "xno"; then
	DEBUG_FLAGS="$DEBUG_FLAGS -DG_DISABLE_CAST_CHECKS"
fi

AC_ARG_ENABLE(asserts,      [  --disable-asserts        compile with GLIB assertions disabled],[asserts=${enableval}],asserts=yes)
if test "x$asserts" = "xno"; then
	DEBUG_FLAGS="$DEBUG_FLAGS -DG_DISABLE_ASSERTS"
fi

AC_ARG_ENABLE(debug,
		[ --enable-debug enable printing of debug messages],
		[ddebug=${enableval}],ddebug=no)
if test "x$ddebug" != "xyes"; then
	CFLAGS="$CFLAGS -DG_DEBUG_DISABLE"
fi

AC_ARG_ENABLE([maemo-launcher],
	[AS_HELP_STRING([--enable-maemo-launcher],
		[build with maemo-launcher support])],
		[case "${enableval}" in
			yes) maemo_launcher=true ;;
			no)  maemo_launcher=false ;;
			*) AC_MSG_ERROR([bad value ${enableval} for --enable-maemo-launcher]) ;;
		esac], [maemo_launcher=false])

if test x$maemo_launcher = xtrue
then
	PKG_CHECK_MODULES(MAEMO_LAUNCHER, [maemo-launcher-app])
	AC_SUBST(MAEMO_LAUNCHER_CFLAGS)
	MAEMO_LAUNCHER_LIBS="-Xcompiler \"$MAEMO_LAUNCHER_LIBS\""
	AC_SUBST(MAEMO_LAUNCHER_LIBS)
	echo "Enabling maemo launcher"
fi

AC_OUTPUT([
	Makefile
	src/Makefile
])

