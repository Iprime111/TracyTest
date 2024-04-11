cmake_minimum_required(VERSION 3.10)
project(Test)

# THIS COMMAND WORKS WELL:
# g++ ../hui.cpp ../tracy/public/TracyClient.cpp -I../tracy/public/tracy -DTRACY_ENABLE -DTRACY_FIBERS -lpthread -ldl

set(THREADS_PREFER_PTHREAD_FLAG ON)
find_package(Threads REQUIRED)

add_executable(Test test.cpp)

set (TRACY_ENABLE 1)

add_subdirectory (tracy)
target_include_directories (Test PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/tracy/public/tracy)

target_link_libraries(Test PUBLIC TracyClient ${CMAKE_DL_LIBS} pthread)
