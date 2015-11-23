###############
#Example Makefile for a c or fortran program linking to libcfd2lcs
#Hopefully, the only thing that needs to change is the 
#line here htat points to libcfd2lcs installation on your machine:
##############
CFD2LCS_HOME = /home/finnj/work/CFD/cfd2lcs/code/libcfd2lcs

include $(CFD2LCS_HOME)/Makefile.in

CFD2LCS_LIBS = -L $(CFD2LCS_HOME)/lib/ -lcfd2lcs -lbspline
CFD2LCS_INC = -$(INC)$(CFD2LCS_HOME)/include/
LIBS = $(CFD2LCS_LIBS) $(THIRD_PARTY_LIBS)

.SUFFIXES:
.SUFFIXES: .c .o
.SUFFIXES: .f90 .o

default:  DOUBLE_GYRE_F90 DOUBLE_GYRE_C ABC_FLOW_F90 ABC_FLOW_C
	$(info ************  COMPILATION SUCCESSFUL ************)


DOUBLE_GYRE_F90: double_gyre_f.o 
	$(F90) -o $@ double_gyre_f.o $(LIBS)
	mkdir -p dump

DOUBLE_GYRE_C: double_gyre_c.o 
	$(CC) -o $@ double_gyre_c.o $(LIBS) $(CLIBS)
	mkdir -p dump

ABC_FLOW_F90: abc_flow_f.o 
	$(F90) -o $@ abc_flow_f.o $(LIBS)
	mkdir -p dump

ABC_FLOW_C: abc_flow_c.o 
	$(CC) -o $@ abc_flow_c.o $(LIBS) $(CLIBS)
	mkdir -p dump


.c.o:
	$(CC) -c $(CFLAGS) -$(INC). $(CFD2LCS_INC) $(THIRD_PARTY_INC) -o $@ $<

.f90.o:
	$(F90) $(FFLAGS) -$(INC). $(CFD2LCS_INC) $(THIRD_PARTY_INC) $*.f90


clean:
	rm -f *.o *.mod DOUBLE_GYRE_F90 DOUBLE_GYRE_C ABC_FLOW_F90 ABC_FLOW_C