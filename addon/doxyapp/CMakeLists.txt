find_package(Iconv)

include_directories(
	${CMAKE_SOURCE_DIR}/src
	${CMAKE_SOURCE_DIR}/libversion
	${GENERATED_SRC}
	${CMAKE_SOURCE_DIR}/qtools
	${ICONV_INCLUDE_DIR}
	${CLANG_INCLUDEDIR}
)

add_executable(doxyapp
doxyapp.cpp
)
add_sanitizers(doxyapp)

if (use_libclang)
    set(CLANG_LIBS libclang clang-cpp ${llvm_libs})
endif()

target_link_libraries(doxyapp
doxymain
qtools
md5
lodepng
mscgen
doxygen_version
doxycfg
vhdlparser
${ICONV_LIBRARIES}
${CMAKE_THREAD_LIBS_INIT}
${SQLITE3_LIBRARIES}
${EXTRA_LIBS}
${CLANG_LIBS}
${COVERAGE_LINKER_FLAGS}
)

install(TARGETS doxyapp DESTINATION bin)
