#######################################################################
# Makefile for lua test-suite
#######################################################################

LANGUAGE     = lua
LUA          = 
SCRIPTSUFFIX = _runme.lua
srcdir       = .
top_srcdir   = ../../..
top_builddir = ../../..

# sorry, currently very few test cases work/have been written

#CPP_TEST_CASES += \
#	cnum 

#C_TEST_CASES += \
#	file_test \
#	nondynamic


include $(srcdir)/../common.mk

# Overridden variables here
LIBS       = -L.

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
# a file is found which has _runme.lua appended after the testcase name.
run_testcase = \
	if [ -f $(srcdir)/$(SCRIPTPREFIX)$*$(SCRIPTSUFFIX) ]; then \
	  env LD_LIBRARY_PATH=.:$$LD_LIBRARY_PATH $(RUNTOOL) $(LUA) $(srcdir)/$(SCRIPTPREFIX)$*$(SCRIPTSUFFIX); \
	fi

# Clean: (does nothing, we dont generate extra lua code)
%.clean:
	

clean:
	$(MAKE) -f $(top_builddir)/$(EXAMPLES)/Makefile lua_clean

cvsignore:
	@echo '*wrap* *.so *.dll *.exp *.lib'
	@echo Makefile
	@for i in ${CPP_TEST_CASES} ${C_TEST_CASES}; do echo $$i.lua; done 
	@for i in ${CPP_TEST_CASES} ${C_TEST_CASES}; do if grep -q $${i}_runme.lua CVS/Entries ; then echo $${i}_runme.lua; fi; done 
