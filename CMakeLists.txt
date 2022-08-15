cmake_minimum_required(VERSION 3.10.0)

project(fast-mass-spring)

set(Sources
    ClothApp/app.cpp
    ClothApp/MassSpringSolver.cpp
    ClothApp/Mesh.cpp
    ClothApp/Renderer.cpp
    ClothApp/Shader.cpp
    ClothApp/UserInteraction.cpp
)

find_package(OpenGL REQUIRED)
include_directories(${OPENGL_INCLUDE_DIRS})

# needed for OpenMesh on Windows
if(WIN32)
  add_definitions(-D_USE_MATH_DEFINES)
endif()

# copy shaders to binary directory
file(INSTALL ClothApp/shaders/ DESTINATION shaders/)

# create executable
add_executable(fast-mass-spring ${Sources})

find_package(GLUT REQUIRED)
target_link_libraries(fast-mass-spring PRIVATE GLUT::GLUT)
find_package(GLEW REQUIRED)
target_link_libraries(fast-mass-spring PRIVATE GLEW::GLEW)
find_package(Eigen3 CONFIG REQUIRED)
target_link_libraries(fast-mass-spring PRIVATE Eigen3::Eigen)
find_package(openmesh REQUIRED)
target_include_directories(fast-mass-spring PRIVATE ${OPENMESH_INCLUDE_DIRS})
target_link_libraries(fast-mass-spring PRIVATE ${OPENMESH_LIBRARIES})
find_package(glm CONFIG REQUIRED)
target_link_libraries(fast-mass-spring PRIVATE glm::glm)