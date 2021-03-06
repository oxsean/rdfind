dnl configure.in for rdfind.
dnl copyright 20016-2017 Paul Dreik (earlier Paul Sundvall)
dnl Distributed under GPL v 2.0 or later, at your option.
dnl See LICENSE for further details.

VERSION="1.3.5"
AC_INIT(rdfind,1.3.5)
AC_CONFIG_SRCDIR(rdfind.cc)
AC_CONFIG_HEADERS(config.h)       

AM_INIT_AUTOMAKE


dnl find and test the C compiler
AC_PROG_CC
AC_PROG_CXX
AC_LANG_CPLUSPLUS
        
AC_PROG_MAKE_SET
               
AC_HEADER_STDC

dnl see if we should run a debug build with lots of output
showdebugmessages=no
AC_ARG_ENABLE(debug,
 	AC_HELP_STRING(
 	    [--enable-debug],
 	    [enable debug printouts in program (default=no)]
 	),
   	showdebugmessages="$enableval"
)
AC_MSG_RESULT($showdebugmessages)
if test x"$showdebugmessages" = x"yes"; then
	AC_DEFINE([RDFIND_DEBUG],[1],[Enable debug printouts in program])
dnl	CXXFLAGS="$CXXFLAGS -g -Wall -Werror"
fi	


dnl test for nettle
AC_CHECK_HEADER(nettle/sha.h,,[AC_MSG_ERROR([
 nettle header files missing. Please install nettle
 first. If you have already done so and get this error message 
 anyway, it may be installed somewhere else, maybe because you 
 don't have root access. Pass CPPFLAGS=-I/your/path/to/nettle to configure
 and try again. The path should be so that #include \"nettle/sha.h\" works.
 On Debian-ish systems, use \"apt-get install nettle-dev\" to get a system
 wide nettle install.
])]) 
AC_CHECK_LIB(nettle,main,,[AC_MSG_ERROR([
 Could not link to libnettle. Please install nettle
 first. If you have already done so; please run ldconfig
 as root or check whether the path libnettle was installed
 to is in your LD_LIBRARY_PATH. If you have nettle 
 somewhere else, maybe because you don't have root 
 access, pass LDFLAGS=-L/your/path/to/nettle to configure
 and try again.
])])

dnl test for some specific functions
AC_CHECK_FUNC(stat,,AC_MSG_ERROR(oops! no stat ?!?))
AC_CHECK_FUNC(nanosleep,,AC_MSG_WARN(cant do nanosleep ?))

AC_CHECK_LIB(stdc++, main,,AC_MSG_ERROR(rdfind requires libstdc++))          

AC_CHECK_HEADERS(string,,AC_MSG_WARN(STL classes missing ?))
AC_CHECK_HEADERS(vector,,AC_MSG_WARN(STL classes missing ?))
AC_CHECK_HEADERS(time.h,,AC_MSG_WARN(nanosleep header time.h missing?))

dnl check for 64 bit support
AC_SYS_LARGEFILE

AC_SUBST(VERSION)

dnl read Makefile.in and write Makefile
AC_OUTPUT(Makefile)
