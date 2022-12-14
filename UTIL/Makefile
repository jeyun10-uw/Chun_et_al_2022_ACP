# Makefile to compile conversion utilities. You need to set include and library paths for NETCDF
#

PLATFORM := $(shell uname -s)

# uncomment line for your platform or add your own:

#---------------------------------------------------------
# AIX 

ifeq ($(PLATFORM),AIX)

LIB_NETCDF = /usr/local/xlf/lib
INC_NETCDF = /usr/local/xlf/include

FF = xlf90_r -qfixed -I$(INC_NETCDF) 
LDFLAGS = -L$(LIB_NETCDF) -lnetcdf

endif
#---------------------------------------------------------
# SGI IRIX64


ifeq ($(PLATFORM),IRIX64)


LIB_NETCDF = /usr/local/lib

FF = f90 -fixedform -extend_source -I$(INC_NETCDF) 
LDFLAGS = -L$(LIB_NETCDF) -lnetcdf

endif
#---------------------------------------------------------
# Mac OS X 


ifeq ($(PLATFORM),Darwin)


INC_NETCDF      := /usr/local/netcdf/include
LIB_NETCDF       := /usr/local/netcdf/lib

FF = mpif90 -fixed -O3 -pad -extend_source -I$(INC_NETCDF)

#FF = mpif90 -fixed -extend_source -I$(INC_NETCDF)

#FF = xlf90 -qfixed -I$(INC_NETCDF) 

#FF = f95 -qfixed -kind=byte -gline -I$(INC_NETCDF) 

#FF = gfortran  -O3 -ffixed-form -ffixed-line-length-0 -I$(INC_NETCDF)

LDFLAGS = -L${LIB_NETCDF} -lnetcdf


endif
#---------------------------------------------------------
#
ifeq ($(PLATFORM),Linux)


# UW Cluster

NCPATH = /usr/local/modules/netcdf/4.6.1.i19/intel/19.0.2
INC_NETCDF   := ${NCPATH}/include
LIB_NETCDF   := ${NCPATH}/lib

FF = ifort -O2 -xHOST -fp-model source -I${INC_NETCDF}
LDFLAGS = -L${LIB_NETCDF} -Wl,-rpath ${LIB_NETCDF} -lnetcdff -lnetcdf


#---------------------------------------------------------
#
# Linux Cluster (seawulf@sunysb)
#

#INC_NETCDF = /nfs/user04/marat/local/include
#LIB_NETCDF = /nfs/user04/marat/local/lib


#FF = ifort -O3 -fixed -extend_source -I${INC_NETCDF}
#LDFLAGS = -L${LIB_NETCDF} -lnetcdf

endif
#---------------------------------------------------------

VPATH = ./SRC

all: bin2D2nc bin3D2nc 2Dbin2nc 2Dbin2nc_mean bin3D2nc_mean com3D2bin 2Dcom2nc 2Dcom2nc_mean com3D2nc com3D2nc_mean com2D2nc stat2nc isccp2nc modis2nc misr2nc com3D2nc_sep 2Dbin2nc_sep 2Dcom_sep2one 2Dbin_sep2one com3D_sep2one bin3D_sep2one glue_movie_raw

.f:   
	$(FF) -o $@ -I./SRC $< ./SRC/hbuf_lib.f ./SRC/cape.f ./SRC/cin.f $(LDFLAGS) 

clean: 
	rm bin* com* stat* 2* isccp* modis* misr* *.o glue*
