cmake_minimum_required(VERSION 3.0)

project(thingy52)

include_directories(includes)
include_directories(includes/src/shared)
include_directories(includes/lib)
include_directories(libmqttclient/MQTTPacket/src)

add_subdirectory(libbluetooth)
add_subdirectory(libshared)
add_subdirectory(libmqttclient)

# thingy.c
add_executable(thingy
    thingy.c)

target_link_libraries(thingy bluetooth shared paho-embed-mqtt3cc paho-embed-mqtt3c jansson)
target_include_directories(thingy PRIVATE "libmqttclient/MQTTClient-C/src" "libmqttclient/MQTTClient-C/src/linux")
target_compile_definitions(thingy PRIVATE MQTTCLIENT_PLATFORM_HEADER=MQTTLinux.h)

install(TARGETS thingy RUNTIME DESTINATION bin)
