#######################################################################
# Makefile for guile test-suite
#######################################################################

LANGUAGE     = guile
VARIANT      = _gh
SCRIPTSUFFIX = _runme.scm
srcdir       = .
top_srcdir   = ../../..
top_builddir = ../../..
GUILE        = 
GUILE_RUNTIME=-runtime

C_TEST_CASES = long_long \
               list_vector \
               multivalue \
               pointer_in_out


include $(srcdir)/../common.mk

# Overridden variables here
# none!

# Custom tests - tests with additional commandline options
%.multicpptest: SWIGOPT += $(GUILE_RUNTIME)

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
# a file is found which has _runme.scm appended after the testcase name.
run_testcase = \
	if [ -f $(srcdir)/$(SCRIPTPREFIX)$*$(SCRIPTSUFFIX) ]; then \
	  env LD_LIBRARY_PATH=.:$$LD_LIBRARY_PATH $(RUNTOOL) $(GUILE) -l $(srcdir)/$(SCRIPTPREFIX)$*$(SCRIPTSUFFIX); \
	fi

# Clean
%.clean:
	@rm -f $*-guile

clean:
	$(MAKE) -f $(top_builddir)/$(EXAMPLES)/Makefile guile_clean
