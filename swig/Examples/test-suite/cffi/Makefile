#######################################################################
# Makefile for cffi test-suite
#######################################################################

LANGUAGE     = cffi
CFFI         = cffi
SCRIPTSUFFIX = _runme.lisp
srcdir       = .
top_srcdir   = ../../..
top_builddir = ../../..

include $(srcdir)/../common.mk

# Overridden variables here
# none!

# Custom tests - tests with additional commandline options
# none!

# Rules for the different types of tests
%.cpptest: 
	$(setup)
	+$(swig_and_compile_cpp)
	$(run_testcase)

%.ctest:
	$(setup)
	+$(swig_and_compile_c)
	$(run_testcase)

%.multicpptest: 
	$(setup)
	+$(swig_and_compile_multi_cpp)
	$(run_testcase)

# Runs the testcase. A testcase is only run if
# a file is found which has _runme.lisp appended after the testcase name.
run_testcase = \
	if [ -f $(srcdir)/$(SCRIPTPREFIX)$*$(SCRIPTSUFFIX) ]; then \
	  env LD_LIBRARY_PATH=.:$$LD_LIBRARY_PATH $(RUNTOOL) $(CFFI) -r $(srcdir)/$(SCRIPTPREFIX)$*$(SCRIPTSUFFIX); \
	fi

# Clean
%.clean:
	

clean:
	$(MAKE) -f $(top_builddir)/$(EXAMPLES)/Makefile cffi_clean
