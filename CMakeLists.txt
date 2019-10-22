
set(PROJECT_NAME bimg)

set(CMAKE_C_COMPILER g++)
add_compile_options(-std=c++1y)

set(BIMG_DIR ${CMAKE_CURRENT_SOURCE_DIR})

set(SRCS_PATH
    "include/bimg"
    "src"
	"3rdparty/astc-codec/src/decoder"
	"3rdparty/astc-codec/src/base"
)

set(INC_DIR 
	${BIMG_DIR}/3rdparty/astc-codec/include
	${BIMG_DIR}/3rdparty/astc-codec
	${BIMG_DIR}/3rdparty/iqa/include
	${BIMG_DIR}/3rdparty
	${BIMG_DIR}/include
	${BIMG_DIR}/../bx/include
)

IF (OS_IS_WINDOWS)
	set(INC_DIR ${INC_DIR} 
		${BIMG_DIR}/../bx/include/compat/msvc
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
aux_add_lib(
	${PROJECT_NAME} "3rd"
	${SRCS_PATH}
)

target_include_directories( ${PROJECT_NAME} PUBLIC ${CMAKE_ROOT_DIR}/3rd/bimg/include )
