set(PROJECT_NAME BlfLogConverter)

set(sources
  BlfLogConverter.cpp
  BlfLogConverterDLL.cpp
  ../../Utility/MultiLanguageSupport.cpp)

set(headers
  BlfLogConverter.h
  Resource.h
  ../../Utility/MultiLanguageSupport.h)

set(resources
  BlfLogConverter.rc)

add_library(${PROJECT_NAME} SHARED ${sources} ${headers} ${resources})

include_directories(
  ${GETTEXT_INCLUDE_DIR}
  ${MFC_INCLUDE_DIRS})

target_link_libraries(${PROJECT_NAME}
  BlfLibrary
  ${GETTEXT_LIBRARY}
  ${MFC_LIBRARIES})

# installer options
add_custom_command(
  TARGET ${PROJECT_NAME}
  POST_BUILD
  COMMAND ${CMAKE_COMMAND} ARGS -E make_directory ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/${CMAKE_BUILD_TYPE}/ConverterPlugins/
  COMMAND ${CMAKE_COMMAND} ARGS -E copy $<TARGET_FILE:${PROJECT_NAME}> ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/${CMAKE_BUILD_TYPE}/ConverterPlugins/
)
