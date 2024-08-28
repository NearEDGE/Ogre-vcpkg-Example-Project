cmake_minimum_required(VERSION 3.20)
project(ExampleProject)

# Find packages
find_package(OGRE REQUIRED COMPONENTS Bites CONFIG)
find_package(pugixml CONFIG REQUIRED)
find_package(assimp CONFIG REQUIRED)

add_executable(ExampleProject "BasicTutorial1.cpp")

target_link_libraries(ExampleProject PRIVATE 
    OgreMain 
    OgreBites 
    Codec_STBI 
    OgrePaging 
    OgreTerrain
    Plugin_DotScene
    pugixml
    assimp::assimp
)

if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET ExampleProject PROPERTY CXX_STANDARD 20)
endif()


# Copy all runtime DLLs
add_custom_command(TARGET ExampleProject POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_RUNTIME_DLLS:ExampleProject> $<TARGET_FILE_DIR:ExampleProject>
    COMMAND_EXPAND_LISTS
)

# Copy Ogre plugins
add_custom_command(TARGET ExampleProject POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy
        $<TARGET_FILE:Plugin_DotScene>
        $<TARGET_FILE:RenderSystem_Direct3D11>
        $<TARGET_FILE:RenderSystem_GL3Plus>
        $<TARGET_FILE:Plugin_ParticleFX>
        $<TARGET_FILE_DIR:ExampleProject>
)

# Copy plugins.cfg
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/plugins.cfg ${CMAKE_CURRENT_BINARY_DIR}/plugins.cfg @ONLY)
add_custom_command(TARGET ExampleProject POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy
        ${CMAKE_CURRENT_SOURCE_DIR}/plugins.cfg
        $<TARGET_FILE_DIR:ExampleProject>
)

# Copy resources.cfg
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/resources.cfg ${CMAKE_CURRENT_BINARY_DIR}/resources.cfg @ONLY)
add_custom_command(TARGET ExampleProject POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy
        ${CMAKE_CURRENT_SOURCE_DIR}/resources.cfg
        $<TARGET_FILE_DIR:ExampleProject>
)