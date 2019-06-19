cmake_minimum_required(VERSION 3.7.2)
project(telepi)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

set(HAVE_LIBBCM_HOST 1)
add_definitions( -DHAVE_LIBBCM_HOST=1 )
set(USE_EXTERNAL_LIBBCM_HOST 1)
add_definitions( -DUSE_EXTERNAL_LIBBCM_HOST=1 )
set(USE_VCHIQ_ARM 1)
add_definitions( -DUSE_VCHIQ_ARM=1 )
set(OMX_SKIP64BIT 1)
add_definitions( -DOMX_SKIP64BIT=1 )

if (EXISTS /opt/vc/include)
    include_directories(/opt/vc/include)
    include_directories(/opt/vc/include/interface/vcos/pthreads)
    include_directories(/opt/vc/include/interface/vmcs_host)
    include_directories(/opt/vc/include/interface/vmcs_host/linux)
    include_directories(/opt/vc/src/hello_pi/libs/ilclient/)

    link_directories(/opt/vc/lib)
    link_directories(/opt/vc/src/hello_pi/libs/ilclient)
else()
    include_directories(../firmware-master/opt/vc/include)
    include_directories(../firmware-master/opt/vc/include/interface/vcos/pthreads)
    include_directories(../firmware-master/opt/vc/include/interface/vmcs_host)
    include_directories(../firmware-master/opt/vc/include/interface/vmcs_host/linux)
    include_directories(../firmware-master/opt/vc/src/hello_pi/libs/ilclient/)

    link_directories(../firmware-master/opt/vc/lib)
    link_directories(../firmware-master/opt/vc/src/hello_pi/libs/ilclient)
endif()

add_executable(telepi telepi.c telepi.h encode.c)
#add_executable(telepi snapshot_resize.c)

# linking will work only on RPi probably...
target_link_libraries(telepi pthread openmaxil bcm_host vcos vchiq_arm ilclient)
