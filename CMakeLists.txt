cmake_minimum_required(VERSION 3.6)
project(PortAudioTest)

set(CMAKE_C_STANDARD 11)

link_directories(lib)
include_directories(include)

find_library(carbon_lib Carbon)
find_library(audiounit_lib Audiounit)
find_library(coreaudio_lib Coreaudio)
find_library(audioToolbox_lib AudioToolbox)
find_library(coreServices_lib CoreServices)

if (NOT carbon_lib)
    message(FATAL_ERROR "carbon_lib not found")
endif ()
if (NOT audiounit_lib)
    message(FATAL_ERROR "AudioUnit not found")
endif ()
if (NOT coreaudio_lib)
    message(FATAL_ERROR "coreaudio_lib not found")
endif ()
if (NOT audioToolbox_lib)
    message(FATAL_ERROR "audioToolbox_lib not found")
endif ()
if (NOT coreServices_lib)
    message(FATAL_ERROR "coreServices_lib not found")
endif ()

set(frameworks
        ${carbon_lib}
        ${audiounit_lib}
        ${coreaudio_lib}
        ${audioToolbox_lib}
        ${coreServices_lib})

set(SourceFuzz pa_fuzz.c)
add_executable(Fuzz ${SourceFuzz})
target_link_libraries(Fuzz libportaudio.a ${frameworks})

set(SourcePink paex_pink.c)
add_executable(Pink ${SourcePink})
target_link_libraries(Pink libportaudio.a ${frameworks})

set(SourceSaw paex_saw.c)
add_executable(Saw ${SourceSaw})
target_link_libraries(Saw libportaudio.a ${frameworks})