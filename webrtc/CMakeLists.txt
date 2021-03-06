cmake_minimum_required(VERSION 3.5)
project(webrtc)

include(LibWebRTCCommand)

if (WIN32)
    set(GCLIENT_EXECUTABLE gclient.bat)
    set(FETCH_EXECUTABLE fetch.bat)
else(WIN32)
    set(GCLIENT_EXECUTABLE gclient)
    set(FETCH_EXECUTABLE fetch)
endif(WIN32)

libwebrtc_command(
    NAME webrtc-ios-fetch
    COMMAND ${FETCH_EXECUTABLE} --nohooks webrtc_ios
    WORKING_DIRECTORY "${CMAKE_BINARY_DIR}"
    COMMENT "Fetching WebRTC iOS"
)

libwebrtc_command(
    NAME webrtc-ios-sync
    COMMAND ${GCLIENT_EXECUTABLE} sync
    WORKING_DIRECTORY "${CMAKE_BINARY_DIR}"
    COMMENT "Synchronizing WebRTC iOS"
    DEPENDS webrtc-ios-fetch
)