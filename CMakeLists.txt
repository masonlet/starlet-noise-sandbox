cmake_minimum_required(VERSION 3.20)

set(PROJ starlet_noise_sandbox)
set(SRC_DIR "${CMAKE_CURRENT_SOURCE_DIR}/src")
set(INC_DIR "${CMAKE_CURRENT_SOURCE_DIR}/inc")
set(ASSET_DIR "${CMAKE_CURRENT_SOURCE_DIR}/assets")

project(${PROJ} LANGUAGES CXX)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_SUPPRESS_REGENERATION ON)

file(GLOB_RECURSE SOURCES CONFIGURE_DEPENDS ${SRC_DIR}/*.cpp)
file(GLOB_RECURSE HEADERS CONFIGURE_DEPENDS ${INC_DIR}/starlet-noise-sandbox/*.hpp)
file(GLOB_RECURSE ASSETS  CONFIGURE_DEPENDS "${ASSET_DIR}/*")

add_executable(${PROJ} ${SOURCES} ${HEADERS})
target_include_directories(${PROJ} PUBLIC "${INC_DIR}")

source_group(TREE ${SRC_DIR} PREFIX "Source Files" FILES ${SOURCES})
source_group(TREE ${INC_DIR} PREFIX "Header Files" FILES ${HEADERS})

add_custom_target(Assets SOURCES ${ASSETS})
set_target_properties(Assets PROPERTIES FOLDER "Assets")
source_group("Assets" FILES ${ASSETS})

include(FetchContent)
FetchContent_Declare(starlet_math
  GIT_REPOSITORY https://github.com/masonlet/starlet-math.git 
  GIT_TAG main
)
FetchContent_MakeAvailable(starlet_math)

target_link_libraries(${PROJ} PUBLIC starlet_math)

set_target_properties(${PROJ} PROPERTIES
  RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
  ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
  LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
  VS_DEBUGGER_WORKING_DIRECTORY "$<TARGET_FILE_DIR:${PROJ}>"
)

set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT ${PROJ})
