cmake_minimum_required (VERSION 2.8.9)

project(paho)

find_package(OpenSSL)
find_package(Threads)

set(VERSION_MAJOR 1)
set(VERSION_MINOR 0)
set(VERSION_STRING ${VERSION_MAJOR}.${VERSION_MINOR})

set(
  COMMON_SOURCE_FILES
  src/Clients.c
  src/Heap.c
  src/LinkedList.c
  src/Log.c
  src/MQTTPacket.c
  src/MQTTPacketOut.c
  src/MQTTPersistence.c
  src/MQTTPersistenceDefault.c
  src/MQTTProtocolClient.c
  src/MQTTProtocolOut.c
  src/Messages.c
  src/Socket.c
  src/SocketBuffer.c
  src/StackTrace.c
  src/Thread.c
  src/Tree.c
  src/utf-8.c
)

set(
  C_SOURCE_FILES
  src/MQTTClient.c
)

set(
  CS_SOURCE_FILES
  src/MQTTClient.c
  src/SSLSocket.c
)

set(
  A_SOURCE_FILES
  src/MQTTAsync.c
)

set(
  AS_SOURCE_FILES
  src/MQTTAsync.c
  src/SSLSocket.c
)

set(CMAKE_MACOSX_RPATH 1)

add_library(paho-common STATIC ${COMMON_SOURCE_FILES})

add_library(paho-mqtt3c SHARED ${C_SOURCE_FILES})
target_link_libraries(
  paho-mqtt3c
  paho-common
  ${CMAKE_THREAD_LIBS_INIT}
)
set_target_properties(
  paho-mqtt3c
  PROPERTIES VERSION ${VERSION_STRING}
             SOVERSION ${VERSION_MAJOR}
)

add_library(paho-mqtt3cs SHARED ${CS_SOURCE_FILES})
target_link_libraries(
  paho-mqtt3cs
  paho-common
  ${CMAKE_THREAD_LIBS_INIT}
)
set_target_properties(
  paho-mqtt3cs
  PROPERTIES VERSION ${VERSION_STRING}
             SOVERSION ${VERSION_MAJOR}
)

add_library(paho-mqtt3a SHARED ${A_SOURCE_FILES})
target_link_libraries(
  paho-mqtt3a
  paho-common
  ${CMAKE_THREAD_LIBS_INIT}
)
set_target_properties(
  paho-mqtt3a
  PROPERTIES VERSION ${VERSION_STRING}
             SOVERSION ${VERSION_MAJOR}
)

add_library(paho-mqtt3as SHARED ${AS_SOURCE_FILES})
target_link_libraries(
  paho-mqtt3as
  paho-common
  ${CMAKE_THREAD_LIBS_INIT}
)
set_target_properties(
  paho-mqtt3as
  PROPERTIES VERSION ${VERSION_STRING}
             SOVERSION ${VERSION_MAJOR}
)

install(
  TARGETS paho-mqtt3c paho-mqtt3cs paho-mqtt3a paho-mqtt3as
  DESTINATION lib
)

install(
  DIRECTORY src/ DESTINATION include
  FILES_MATCHING PATTERN "*.h"
)
