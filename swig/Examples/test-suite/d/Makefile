#######################################################################
# Makefile for D test-suite
#######################################################################

LANGUAGE     = d
srcdir       = .
top_srcdir   = ../../../..
top_builddir = ../../../..

ifeq (2,$(D_VERSION))
  VERSIONSUFFIX = .2
else
  VERSIONSUFFIX = .1
endif

TESTSUFFIX = _runme$(VERSIONSUFFIX).d

CPP_TEST_CASES = \
	d_exception_name \
	d_nativepointers \
	exception_partial_info

include $(srcdir)/../common.mk

# Override some variables from common.mk:

TARGETSUFFIX = _wrap

SWIGOPT+=-splitproxy -package $*

# Rules for the different types of tests
%.cpptest:
	$(setup)
	+(cd $*$(VERSIONSUFFIX) && $(swig_and_compile_cpp))
	+$(run_testcase)

%.ctest:
	$(setup)
	+(cd $*$(VERSIONSUFFIX) && $(swig_and_compile_c))
	+$(run_testcase)

%.multicpptest:
	$(setup)
	+(cd $*$(VERSIONSUFFIX) && $(swig_and_compile_multi_cpp))
	+$(run_testcase)

# Makes a directory for the testcase if it does not exist
setup = \
	if [ -f $(srcdir)/$(TESTPREFIX)$*$(TESTSUFFIX) ]; then			\
	  echo "$(ACTION)ing testcase $* (with run test) under $(LANGUAGE)" ;	\
	else									\
	  echo "$(ACTION)ing testcase $* under $(LANGUAGE)" ;			\
	fi;									\
	if [ ! -d $*$(VERSIONSUFFIX) ]; then					\
	  mkdir $*$(VERSIONSUFFIX);						\
	fi;									\
	if [ ! -d $*$(VERSIONSUFFIX)/$* ]; then					\
	  mkdir $*$(VERSIONSUFFIX)/$*;						\
	fi

# Compiles D files then runs the testcase. A testcase is only run if
# a file is found which has _runme.d appended after the testcase name.
run_testcase = \
	if [ -f $(srcdir)/$(TESTPREFIX)$*$(TESTSUFFIX) ]; then \
	  cd $*$(VERSIONSUFFIX) && \
	  $(MAKE) -f $(top_builddir)/$(EXAMPLES)/Makefile \
	  DFLAGS='-of$*_runme' \
	  DSRCS='../$(srcdir)/$(TESTPREFIX)$*$(TESTSUFFIX) `find $* -name *.d`' d_compile && \
	  env LD_LIBRARY_PATH=".:$$LD_LIBRARY_PATH" $(RUNTOOL) ./$*_runme; \
	else \
	  cd $*$(VERSIONSUFFIX) && \
	  $(MAKE) -f $(top_builddir)/$(EXAMPLES)/Makefile \
	  DFLAGS='-c' \
	  DSRCS='`find $* -name *.d`' d_compile && cd .. ; \
	fi

# Clean: remove testcase directories
%.clean:
	@if [ -d $*$(VERSIONSUFFIX) ]; then \
	  rm -rf $*$(VERSIONSUFFIX); \
	fi
