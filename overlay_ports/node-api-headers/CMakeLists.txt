cmake_minimum_required(VERSION 3.19)
project(nodelib C)

add_custom_target(nodelib ALL DEPENDS ${CMAKE_CURRENT_BINARY_DIR}/node.lib)
add_custom_command(
  OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/node.lib
  COMMAND ${CMAKE_AR}
          /def:${CMAKE_CURRENT_SOURCE_DIR}/def/node_api.def
          /out:${CMAKE_CURRENT_BINARY_DIR}/node.lib
          ${CMAKE_STATIC_LINKER_FLAGS}
          $<$<CONFIG:Debug>:${CMAKE_STATIC_LINKER_FLAGS_DEBUG}>
          $<$<CONFIG:Release>:${CMAKE_STATIC_LINKER_FLAGS_RELEASE}>
  COMMENT "Building import library for NodeJS"
)

install(FILES ${CMAKE_BINARY_DIR}/node.lib DESTINATION lib)
