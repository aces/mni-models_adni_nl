# Require autoconf 2.57 or newer.
AC_PREREQ([2.57])

# The arguments are package name, and package version.
AC_INIT([mni-models_adni_nl],[1.3],[Claude Lepage <claude@bic.mni.mcgill.ca>])
AC_CONFIG_SRCDIR([epm-header.in])

AM_INIT_AUTOMAKE

# The argument is the name of the generated header file.
# It is recommended to leave it as "config.h".
AC_CONFIG_HEADERS([config.h])

# Checks for programs.
AC_PROG_INSTALL
AC_PROG_GZIP

# check for make_model
AC_PROG_MAKE_MODEL

# Finish up by writing output files.
AC_CONFIG_FILES([Makefile])
AC_OUTPUT(epm-header
)
