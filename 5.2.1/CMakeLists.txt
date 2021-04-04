cmake_minimum_required (VERSION 3.8)

project (GifLib 
        VERSION 5.2.1
        )

include_directories(${PROJECT_SOURCE_DIR}/source)
aux_source_directory(${PROJECT_SOURCE_DIR}/source source_files)

set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)
set(CMAKE_INSTALL_PREFIX ${PROJECT_SOURCE_DIR})
file(GLOB head_files "${PROJECT_SOURCE_DIR}/source/*.h")

add_library(GifLib STATIC ${head_files} ${source_files})
install(FILES ${head_files} DESTINATION include)

IF (MSVC)
#  add_definitions(-D_CRT_NONSTDC_NO_DEPRECATE)
#  add_definitions(-D_CRT_SECURE_NO_WARNINGS)
  set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /MD")
  set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} /MDd")
  set(build_flags "-D_CRT_NONSTDC_NO_DEPRECATE -D_CRT_SECURE_NO_WARNINGS")
  set_target_properties(GifLib PROPERTIES COMPILE_FLAGS ${build_flags})
ENDIF ()
