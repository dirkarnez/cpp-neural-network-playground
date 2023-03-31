cmake_minimum_required(VERSION 3.14)

project("cpp-neural-network-playground")

# This is required
set(SFML_STATIC_LIBRARIES TRUE)

find_package(SFML 2.5.1 EXACT COMPONENTS system window graphics REQUIRED)

# uncomment this line if using msvc
# SET(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} /subsystem:windows /ENTRY:mainCRTStartup")

# uncomment this line if using clang
SET(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -static -Wl,--subsystem,windows")

# link_directories(SFML_LIBRARY_DIR)
# link_directories(SFML_INCLUDE_DIR)

add_executable(${PROJECT_NAME} 
    "src/main.cpp"
    "src/ActivationFunction.cpp"
    "src/BackPropagation.cpp"
    "src/DrawNeuralNetwork.cpp"
    "src/DrawText.cpp"
    "src/ForwardPropagation.cpp"
    "src/GetMaxElement.cpp"
    "src/GetMinElement.cpp"
    "src/Main.cpp"
)

target_include_directories(${PROJECT_NAME} PRIVATE
    "include"
)

add_custom_command(
        TARGET ${PROJECT_NAME} POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_directory
                ${CMAKE_SOURCE_DIR}/resources
                ${CMAKE_CURRENT_BINARY_DIR}/resources)

target_link_libraries(${PROJECT_NAME} sfml-graphics)