add_library(elfutil SHARED
    elfutil/elffile.cpp
    elfutil/log.cpp
    elfutil/errors.cpp
)

target_include_directories(elfutil
    PUBLIC $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
    PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}
)

set(elfutil_PUBLIC_HEADER
    ${PROJECT_SOURCE_DIR}/include/elfutil/elffile.h;
    ${PROJECT_SOURCE_DIR}/include/elfutil/errors.h;
)

set_target_properties(elfutil PROPERTIES
    VERSION ${libelfutil_VERSION} SOVERSION ${libelfutil_VERSION_MAJOR}
    PUBLIC_HEADER "${elfutil_PUBLIC_HEADER}"
)

target_link_libraries(elfutil PUBLIC ${Boost_LIBRARIES})

install(TARGETS elfutil
    EXPORT ElfUtilTargets
    LIBRARY DESTINATION "${INSTALL_LIB_DIR}" COMPONENT lib
    PUBLIC_HEADER DESTINATION "${INSTALL_INCLUDE_DIR}/elfutil" COMPONENT dev
)
