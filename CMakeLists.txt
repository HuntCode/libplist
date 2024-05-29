# For VS2019 and Xcode 12+ support.
cmake_minimum_required(VERSION 3.19 FATAL_ERROR)

# Custom config

project(plist)

if(CMAKE_SYSTEM_NAME STREQUAL "Android")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -O2 -g  -fno-strict-aliasing  -D_GNU_SOURCE  -DHAVE_IPV6  -DHAVE_LINUX  -DNOT_HAVE_SA_LEN  -DPLATFORM_NO_RLIMIT  -DTARGET_OS_LINUX  -DUSES_NETLINK  -DMDNS_DEBUGMSGS=0 -W  -Wall  -Wextra  -Wno-array-bounds  -Wno-pointer-sign  -Wno-unused  -Wno-unused-parameter  -Werror=implicit-function-declaration")
add_definitions(-DHAVE_STRNDUP )
endif()

#
# Sources
#

# libcnary
if(CMAKE_SYSTEM_NAME STREQUAL "Android")
    set(LIBCNARY_SOURCES ${LIBCNARY_SOURCES} 
        libcnary/cnary.c
        libcnary/node.c
        libcnary/node_list.c
    )
endif()

# libplist
if(CMAKE_SYSTEM_NAME STREQUAL "Android")
    set(LIBPLIST_SOURCES ${LIBPLIST_SOURCES} 
        src/Array.cpp
        src/base64.c
        src/Boolean.cpp
        src/bplist.c
		src/bytearray.c
		src/Data.cpp
		src/Date.cpp
		src/Dictionary.cpp
		src/hashtable.c
		src/Integer.cpp
		src/jplist.c
		src/jsmn.c
		src/Key.cpp
		src/Node.cpp
		src/oplist.c
		src/out-default.c
		src/out-limd.c
		src/out-plutil.c
		src/plist.c
		src/ptrarray.c
		src/Real.cpp
		src/String.cpp
		src/Structure.cpp
		src/time64.c
		src/Uid.cpp
		src/xplist.c
    )
endif()

# all sources
if(CMAKE_SYSTEM_NAME STREQUAL "Android")
	set(LIBPLIST_PROJECT_SOURCES
		${LIBCNARY_SOURCES}
		${LIBPLIST_SOURCES}
	)
	set(LIBPLIST_PROJECT_NAME plist)
endif()

add_library(${LIBPLIST_PROJECT_NAME} SHARED ${LIBPLIST_PROJECT_SOURCES})

if(CMAKE_SYSTEM_NAME STREQUAL "Android")
    target_include_directories(${LIBPLIST_PROJECT_NAME} PRIVATE libcnary/include include src)
endif()
