cmake_minimum_required (VERSION 2.8.10)
PROJECT (HDF4_HDF_TEST C CXX)

#-----------------------------------------------------------------------------
# Setup include Directories
#-----------------------------------------------------------------------------
INCLUDE_DIRECTORIES (
    ${CMAKE_Fortran_MODULE_DIRECTORY}
    ${HDF4_HDF_BINARY_DIR}
    ${HDF4_HDFSOURCE_DIR}
)
LINK_DIRECTORIES (
    ${CMAKE_Fortran_MODULE_DIRECTORY}
    ${HDF4_HDF_BINARY_DIR}
    ${CMAKE_LIBRARY_OUTPUT_DIRECTORY}
)

SET (testhdf_SRCS
    ${HDF4_HDF_TEST_SOURCE_DIR}/testhdf.c 
    ${HDF4_HDF_TEST_SOURCE_DIR}/an.c 
    ${HDF4_HDF_TEST_SOURCE_DIR}/anfile.c
    ${HDF4_HDF_TEST_SOURCE_DIR}/bitio.c  
    ${HDF4_HDF_TEST_SOURCE_DIR}/blocks.c
    ${HDF4_HDF_TEST_SOURCE_DIR}/chunks.c  
    ${HDF4_HDF_TEST_SOURCE_DIR}/comp.c 
    ${HDF4_HDF_TEST_SOURCE_DIR}/conv.c 
    ${HDF4_HDF_TEST_SOURCE_DIR}/extelt.c 
    ${HDF4_HDF_TEST_SOURCE_DIR}/file.c 
    ${HDF4_HDF_TEST_SOURCE_DIR}/file1.c 
    ${HDF4_HDF_TEST_SOURCE_DIR}/litend.c 
    ${HDF4_HDF_TEST_SOURCE_DIR}/macros.c 
    ${HDF4_HDF_TEST_SOURCE_DIR}/man.c 
    ${HDF4_HDF_TEST_SOURCE_DIR}/mgr.c 
    ${HDF4_HDF_TEST_SOURCE_DIR}/nbit.c 
    ${HDF4_HDF_TEST_SOURCE_DIR}/rig.c
    ${HDF4_HDF_TEST_SOURCE_DIR}/sdmms.c
    ${HDF4_HDF_TEST_SOURCE_DIR}/sdnmms.c 
    ${HDF4_HDF_TEST_SOURCE_DIR}/sdstr.c
    ${HDF4_HDF_TEST_SOURCE_DIR}/slab.c
    ${HDF4_HDF_TEST_SOURCE_DIR}/tattdatainfo.c
    ${HDF4_HDF_TEST_SOURCE_DIR}/tbv.c
    ${HDF4_HDF_TEST_SOURCE_DIR}/tdatainfo.c
    ${HDF4_HDF_TEST_SOURCE_DIR}/tdfr8.c
    ${HDF4_HDF_TEST_SOURCE_DIR}/tdupimgs.c
    ${HDF4_HDF_TEST_SOURCE_DIR}/tmgrattr.c
    ${HDF4_HDF_TEST_SOURCE_DIR}/tmgrcomp.c
    ${HDF4_HDF_TEST_SOURCE_DIR}/tree.c
    ${HDF4_HDF_TEST_SOURCE_DIR}/tszip.c
    ${HDF4_HDF_TEST_SOURCE_DIR}/tusejpegfuncs.c
    ${HDF4_HDF_TEST_SOURCE_DIR}/tutils.c
    ${HDF4_HDF_TEST_SOURCE_DIR}/tvattr.c
    ${HDF4_HDF_TEST_SOURCE_DIR}/tvnameclass.c
    ${HDF4_HDF_TEST_SOURCE_DIR}/tvset.c
    ${HDF4_HDF_TEST_SOURCE_DIR}/tvsfpack.c
    ${HDF4_HDF_TEST_SOURCE_DIR}/vers.c
  )

IF (WIN32 AND NOT CYGWIN)
  ADD_DEFINITIONS (-DDOS_FS)
ENDIF (WIN32 AND NOT CYGWIN)

#-- Adding test for testhdf
ADD_EXECUTABLE (testhdf ${testhdf_SRCS})
TARGET_NAMING (testhdf ${LIB_TYPE})
TARGET_C_PROPERTIES (testhdf " " " ")
TARGET_LINK_LIBRARIES (testhdf ${HDF4_SRC_LIB_TARGET} ${LINK_LIBS})

#-- Adding test for buffer
IF (NOT WIN32)
  ADD_EXECUTABLE (buffer ${HDF4_HDF_TEST_SOURCE_DIR}/buffer.c)
  TARGET_NAMING (buffer ${LIB_TYPE})
  TARGET_C_PROPERTIES (buffer " " " ")
  TARGET_LINK_LIBRARIES (buffer ${HDF4_SRC_LIB_TARGET} ${LINK_LIBS})
ENDIF (NOT WIN32)

##############################################################################
##############################################################################
###           T H E   T E S T S                                            ###
##############################################################################
##############################################################################

INCLUDE (CMakeTests.cmake)

