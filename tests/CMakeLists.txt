add_executable(usmapgen-enum-tests Enum.cpp)
target_link_libraries(usmapgen-enum-tests PRIVATE UsmapGen::UsmapGen)
target_compile_options(usmapgen-enum-tests PRIVATE -Wall -Wextra -fno-exceptions -fno-rtti)
add_test(NAME enum-max COMMAND usmapgen-enum-tests)

add_executable(usmapgen-name-tests Name.cpp)
target_link_libraries(usmapgen-name-tests PRIVATE UsmapGen::UsmapGen)
target_compile_options(usmapgen-name-tests PRIVATE -Wall -Wextra -fno-exceptions -fno-rtti)
add_test(NAME enum-name-casing COMMAND usmapgen-name-tests)

add_executable(usmapgen-api-tests Api.cpp)
target_link_libraries(usmapgen-api-tests PRIVATE UsmapGen::UsmapGen)
target_compile_options(usmapgen-api-tests PRIVATE -Wall -Wextra -fno-exceptions -fno-rtti)
add_test(NAME api-compatibility COMMAND usmapgen-api-tests)

add_executable(usmapgen-deferred-tests Deferred.cpp)
target_link_libraries(usmapgen-deferred-tests PRIVATE UsmapGen::UsmapGen)
target_compile_options(usmapgen-deferred-tests PRIVATE -Wall -Wextra -fno-exceptions -fno-rtti)
add_test(NAME deferred-registration COMMAND usmapgen-deferred-tests)

add_executable(usmapgen-delegate-tests Delegate.cpp)
target_link_libraries(usmapgen-delegate-tests PRIVATE UsmapGen::UsmapGen)
target_compile_options(usmapgen-delegate-tests PRIVATE -Wall -Wextra -fno-exceptions -fno-rtti)
add_test(NAME delegate-policy COMMAND usmapgen-delegate-tests)

if(USMAPGEN_BUILD_TOOLS)
    add_test(NAME command-line COMMAND ${CMAKE_COMMAND}
        "-DUSMAPGEN=$<TARGET_FILE:usmapgen>"
        "-DUSMAPGEN_EMULATOR=$<TARGET_GENEX_EVAL:usmapgen,$<TARGET_PROPERTY:usmapgen,CROSSCOMPILING_EMULATOR>>"
        -P ${CMAKE_CURRENT_SOURCE_DIR}/CommandLine.cmake)
endif()
