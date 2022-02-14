cmake_minimum_required(VERSION 3.10)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(SealPIR VERSION 2.1 LANGUAGES CXX)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

include_directories( ${CMAKE_SOURCE_DIR}/*.hpp)

add_executable(main 
	main.cpp
)

add_library(sealpir STATIC
  pir.cpp
  pir_client.cpp
  pir_server.cpp
)

option(DEBUG "help string describing option" True)
find_package(SEAL 3.2.0 EXACT REQUIRED)
if(SEAL_FOUND)
  include_directories("/usr/local/include/")
else()
  message(STATUS "SEAL NOT Found !")
endif(SEAL_FOUND)
  
target_link_libraries(main sealpir SEAL::seal)
