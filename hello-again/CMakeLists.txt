project (hello-again)

cmake_minimum_required (VERSION 2.6)

list (APPEND CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake)

set (DATADIR "${CMAKE_INSTALL_PREFIX}/share")

set (PKGDATADIR "${DATADIR}/hello-again")

set (EXEC_NAME "hello-again")
set (RELEASE_NAME "A hello world.")
set (VERSION "0.1")
set (VERSION_INFO "whats up world")

find_package (PkgConfig)

pkg_check_modules (DEPS REQUIRED gtk+-3.0)

add_definitions (${DEPS_CFLAGS})
link_libraries (${DEpS_LIBRARIES})
link_directories (${DEPS_LIBRARY_DIRS})

find_package(Vala REQUIRED)

include(ValaVersion)

ensure_vala_version("0.16" MINIMUM)

include(ValaPrecompile)

vala_precompile(VALA_C ${EXEC_NAME}
    src/hello-again.vala

PACKAGES
    gtk+-3.0
)

add_executable(${EXEC_NAME} ${VALA_C})

install (TARGETS ${EXEC_NAME} RUNTIME DESTINATION bin)

install (FILES ${CMAKE_CURRENT_SOURCE_DIR}/data/hello.desktop DESTINATION ${DATADIR}/applications/)
