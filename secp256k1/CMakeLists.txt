cmake_minimum_required(VERSION 3.4)
project(secp256k1)

find_package(GMP REQUIRED)

add_library(secp256k1 STATIC
  upstream/src/secp256k1.c
  upstream/contrib/lax_der_parsing.c
  upstream/contrib/lax_der_privatekey_parsing.c
)

target_include_directories(secp256k1
    PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/upstream/
        ${CMAKE_CURRENT_SOURCE_DIR}/upstream/include
        ${CMAKE_CURRENT_SOURCE_DIR}/upstream/contrib
    PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/upstream/src
        ${CMAKE_CURRENT_SOURCE_DIR}
        ${GMP_INCLUDE_DIR}
)

target_compile_definitions(secp256k1 PRIVATE HAVE_CONFIG_H=1)

target_link_libraries(secp256k1 ${GMP_LIBRARIES})
install( TARGETS secp256k1
   RUNTIME DESTINATION ${CMAKE_INSTALL_FULL_BINDIR}
   LIBRARY DESTINATION ${CMAKE_INSTALL_FULL_LIBDIR}
   ARCHIVE DESTINATION ${CMAKE_INSTALL_FULL_LIBDIR}
)
