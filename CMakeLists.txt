#
# project: fips-tinycthread
#

if (NOT FIPS_IMPORT)
    cmake_minimum_required(VERSION 2.8)
    get_filename_component(FIPS_ROOT_DIR "../fips" ABSOLUTE)
    include("${FIPS_ROOT_DIR}/cmake/fips.cmake")
    fips_setup(PROJECT fips-tinycthread)
endif()

fips_begin_lib(tinycthread)
    find_package(Threads REQUIRED)
    include_directories(tinycthread/source)
    fips_dir(tinycthread/source)
    fips_files(
        tinycthread.h
        tinycthread.c
    )
fips_end_lib()

if (NOT FIPS_IMPORT)
    fips_begin_app(hello cmdline)
        fips_dir(tinycthread/test)
        fips_files(
            hello.c
        )
        fips_deps(tinycthread)
    fips_end_app()
    fips_begin_app(test cmdline)
        fips_dir(tinycthread/test)
        fips_files(
            test.c
        )
        fips_deps(tinycthread)
    fips_end_app()
    fips_finish()
endif()
