cmake_minimum_required(VERSION 3.18)

project(aeon
    VERSION 0.1.0
    DESCRIPTION "An experimental graphical frontend for the Hastur browser engine"
    HOMEPAGE_URL "https://github.com/zer0-one/aeon"
    LANGUAGES CXX
)

include(GNUInstallDirs)
include(FindPkgConfig)

# Check for dependencies
pkg_check_modules(GTK4 REQUIRED IMPORTED_TARGET gtk4)

# Set options
option(AEON_TEST "Enable unit tests" OFF)

add_executable(aeon
    src/main.cpp
)

target_link_libraries(aeon PUBLIC
    PkgConfig::GTK4
)

target_compile_features(aeon
    PUBLIC cxx_std_20
)

set_target_properties(aeon
    PROPERTIES
        VERSION ${PROJECT_VERSION}
        SOVERSION ${PROJECT_VERSION_MAJOR}
        #CXX_STANDARD 20
        CXX_STANDARD_REQUIRED TRUE
        CXX_EXTENSIONS OFF
        RUNTIME_OUTPUT_DIRECTORY bin
)

# If tests are enabled, make tests
#if(AEON_TEST)
#    enable_testing()
#
#    add_test(NAME muh_test)
#endif()

install(
    TARGETS aeon DESTINATION ${CMAKE_INSTALL_BINDIR}
)

# Install example data, docs, w/e
#install(
#    FILES ${CMAKE_CURRENT_BINARY_DIR}/doc/muh_docs
#    DESTINATION ${CMAKE_INSTALL_DOCDIR}/aeon
#)
