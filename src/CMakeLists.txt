
set(PROJECT_NAME bimg)

set(CMAKE_C_COMPILER g++)
add_compile_options(-std=c++1y)

set(INCROOT ${CMAKE_CURRENT_LIST_DIR}/../include/bimg)
set(SRCROOT ${CMAKE_CURRENT_LIST_DIR})
set(ASTC_DECODE_ROOT ${CMAKE_CURRENT_LIST_DIR}/../3rdparty/astc-codec/src/decoder)
set(ASTC_BASE_ROOT ${CMAKE_CURRENT_LIST_DIR}/../3rdparty/astc-codec/src/base)

set(DIR_SRCS 
	${INCROOT}/bimg.h
	${INCROOT}/decode.h
	${INCROOT}/encode.h
	${SRCROOT}/bimg_p.h
	${SRCROOT}/image.cpp
	${SRCROOT}/image_cubemap_filter.cpp
	${SRCROOT}/image_decode.cpp
	${SRCROOT}/image_gnf.cpp
)

set(ASTC_DECODE_SRC
					${ASTC_DECODE_ROOT}/astc_file.cc
					${ASTC_DECODE_ROOT}/astc_file.h
					${ASTC_DECODE_ROOT}/codec.cc
					${ASTC_DECODE_ROOT}/codec.h
					${ASTC_DECODE_ROOT}/endpoint_codec.cc
					${ASTC_DECODE_ROOT}/endpoint_codec.h
					${ASTC_DECODE_ROOT}/footprint.cc
					${ASTC_DECODE_ROOT}/footprint.h
					${ASTC_DECODE_ROOT}/integer_sequence_codec.cc
					${ASTC_DECODE_ROOT}/integer_sequence_codec.h
					${ASTC_DECODE_ROOT}/intermediate_astc_block.cc
					${ASTC_DECODE_ROOT}/intermediate_astc_block.h
					${ASTC_DECODE_ROOT}/logical_astc_block.cc
					${ASTC_DECODE_ROOT}/logical_astc_block.h
					${ASTC_DECODE_ROOT}/partition.cc
					${ASTC_DECODE_ROOT}/partition.h
					${ASTC_DECODE_ROOT}/physical_astc_block.cc
					${ASTC_DECODE_ROOT}/physical_astc_block.h
					${ASTC_DECODE_ROOT}/quantization.cc
					${ASTC_DECODE_ROOT}/quantization.h
					${ASTC_DECODE_ROOT}/weight_infill.cc
					${ASTC_DECODE_ROOT}/weight_infill.h
					${ASTC_DECODE_ROOT}/types.h	 
)
source_group("astc-decode" FILES ${ASTC_DECODE_SRC})	

set(ASTC_BASE_SRC
				${ASTC_BASE_ROOT}/bit_stream.h
				${ASTC_BASE_ROOT}/bottom_n.h
				${ASTC_BASE_ROOT}/math_utils.h
				${ASTC_BASE_ROOT}/optional.h
				${ASTC_BASE_ROOT}/string_utils.h
				${ASTC_BASE_ROOT}/type_traits.h
				${ASTC_BASE_ROOT}/uint128.h
				${ASTC_BASE_ROOT}/utils.h
)
source_group("astc-base" FILES ${ASTC_BASE_SRC})	
 
set(INC_DIR 
	${CMAKE_CURRENT_LIST_DIR}/../3rdparty/astc-codec/include
	${CMAKE_CURRENT_LIST_DIR}/../3rdparty/astc-codec
	${CMAKE_CURRENT_LIST_DIR}/../3rdparty
	${CMAKE_CURRENT_LIST_DIR}/../include
	${CMAKE_CURRENT_LIST_DIR}/../../bx/include
)

IF (${THE_PROJECT_PREFIX}_OS_WINDOWS)
	set(INC_DIR ${INC_DIR} 
		${CMAKE_CURRENT_LIST_DIR}/../../bx/include/compat/msvc
	)	
ENDIF()

include_directories(${INC_DIR})

Add_Definitions(-D__STDC_LIMIT_MACROS
				-D__STDC_FORMAT_MACROS
				-D__STDC_CONSTANT_MACROS
				-D_HAS_EXCEPTIONS=0
				-D_HAS_ITERATOR_DEBUGGING=0
				-D_ITERATOR_DEBUG_LEVEL=0
				-D_SCL_SECURE=0
				-D_SECURE_SCL=0
				-D_SCL_SECURE_NO_WARNINGS
				-D_CRT_SECURE_NO_WARNINGS
				-D_CRT_SECURE_NO_DEPRECATE
				)

add_lib(
				${PROJECT_NAME} 
				FOLDER "libs" 
				SOURCES ${DIR_SRCS} ${ASTC_DECODE_SRC} ${ASTC_BASE_SRC}
)

