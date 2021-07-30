
include ./Makefile.inc

AR = ar rcs

FPP_DEFINES     = -D_LAGRANGIAN_GLOBAL_ -D_USE_NIX -D_STACK_LIMITS_ -D_USE_PROJ4

CCFLAGS         = ${WARNINGS_FLAGS} ${DEBUG_FLAGS} ${LANG_FLAGS} ${OPT_FLAGS} ${OTH_FLAGS} ${FPP_DEFINES}
OBJ_CCFLAGS     = $(CCFLAGS) -I$(INC_HDF5) -I$(INC_NETCDF) -I$(INC_PROJ4) -I$(INC_PROJ4F) -Iinclude -I../Mohid_Base_1/include -I../Mohid_Base_2/include

OBJ             = build/ModuleHorizontalGrid.o build/ModuleGridData.o  \
                  build/ModuleMM5Format.o build/ModuleEUCenterFormat.o build/ModuleERA40Format.o


.PHONY: clean all

all: bin/ConvertToHDF5.exe

bin/ConvertToHDF5.exe: ${OBJ}
	${FC} ${OBJ_CCFLAGS} $? src/ConvertToHDF5.F90 ${LIBS} -o bin/ConvertToHDF5.exe

build/ModuleHorizontalGrid.o: src/ModuleHorizontalGrid.F90
	${FC} -c $? ${OBJ_CCFLAGS} ${LIBS} -o $@ ${MODOUT}include

build/ModuleGridData.o: src/ModuleGridData.F90
	${FC} -c $? ${OBJ_CCFLAGS} ${LIBS} -o $@ ${MODOUT}include

build/ModuleMM5Format.o: src/ModuleMM5Format.F90
	${FC} -c $? ${OBJ_CCFLAGS} ${LIBS} -o $@ ${MODOUT}include

build/ModuleEUCenterFormat.o: src/ModuleEUCenterFormat.F90
	${FC} -c $? ${OBJ_CCFLAGS} ${LIBS} -o $@ ${MODOUT}include

build/ModuleERA40Format.o: src/ModuleERA40Format.F90
	${FC} -c $? ${OBJ_CCFLAGS} ${LIBS} -o $@ ${MODOUT}include



install:
	ln -sf ../src/ConvertToHDF5/bin/ConvertToHDF5.exe ../../bin/ConvertToHDF5.exe

clean:
	-rm -f build/*.o
	-rm -f include/*.mod
	-rm -f bin/*.exe
