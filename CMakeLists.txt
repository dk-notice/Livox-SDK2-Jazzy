cmake_minimum_required(VERSION 3.8)

project(livox_sdk2)

find_package(ament_cmake REQUIRED)

set(CMAKE_CXX_STANDARD 11)

message(STATUS "main project dir: " ${PROJECT_SOURCE_DIR})

if (CMAKE_CROSSCOMPILING)
	set(THREADS_PTHREAD_ARG
		"PLEASE_FILL_OUT-FAILED_TO_RUN"
		CACHE STRING "Result from TRY_RUN" FORCE)
endif()

if (UNIX)
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pthread")
endif(UNIX)

add_subdirectory(sdk_core)
# add_subdirectory(samples) # Comment out samples for now, focus on core library

# Export targets
install(
  EXPORT sdk_core_targets
  FILE livox_sdk2Targets.cmake
  NAMESPACE livox_sdk2::
  DESTINATION share/${PROJECT_NAME}/cmake
)

ament_export_targets(sdk_core_targets HAS_LIBRARY_TARGET)
ament_export_dependencies(ament_cmake)

ament_package()
