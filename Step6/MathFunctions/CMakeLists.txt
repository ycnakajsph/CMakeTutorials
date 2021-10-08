set(TableSize 20 )

add_executable(MakeTable MakeTable.cxx)

add_custom_command(
  OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/Table.h
  COMMAND MakeTable ${CMAKE_CURRENT_BINARY_DIR}/Table.h ${TableSize}
  DEPENDS MakeTable
)

configure_file(MathFunctions.h.in MathFunctions.h @ONLY)

add_library(MathFunctions mysqrt.cxx ${CMAKE_CURRENT_BINARY_DIR}/Table.h)

# state that anybody linking to us needs to include the current source dir
# to find MathFunctions.h, while we don't.
target_include_directories(MathFunctions
          INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}
          PUBLIC ${CMAKE_CURRENT_BINARY_DIR}
          )

# install rules
install(TARGETS MathFunctions DESTINATION lib)
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/MathFunctions.h DESTINATION include)
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/Table.h DESTINATION include)
