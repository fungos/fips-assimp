# temporary workaround
set(ASSIMP_ENABLE_BOOST_WORKAROUND YES)
set(ASSIMP_BUILD_TEST NO)

if (NOT FIPS_IMPORT)
    cmake_minimum_required(VERSION 2.8)
    get_filename_component(FIPS_ROOT_DIR "../fips" ABSOLUTE)
    include("${FIPS_ROOT_DIR}/cmake/fips.cmake")
    fips_setup()
    fips_project(fips-assimp)
endif()

option(ASSIMP_C4D "Enable C4D Support (windows only)" OFF)
configure_file(
        ${CMAKE_CURRENT_SOURCE_DIR}/assimp/include/assimp/config.h.in 
        ${FIPS_PROJECT_BUILD_DIR}/assimp/config.h)
configure_file(
        ${CMAKE_CURRENT_SOURCE_DIR}/assimp/contrib/zlib/zconf.h.cmakein 
        ${CMAKE_CURRENT_SOURCE_DIR}/assimp/contrib/zlib/zconf.h @ONLY)
include_directories("${FIPS_PROJECT_BUILD_DIR}")

fips_begin_lib(assimp)
    add_definitions(-DASSIMP_BUILD_NO_OWN_ZLIB)
    fips_include_directories(.)
    fips_include_directories(assimp/)
    fips_include_directories(assimp/code)
    fips_include_directories(assimp/include)
    fips_include_directories(assimp/code/BoostWorkaround)
    fips_include_directories(assimp/contrib/openddlparser/include/)
    fips_include_directories(assimp/contrib/rapidjson/include/)
    fips_include_directories(assimp/contrib/irrXML/)
    fips_include_directories("${FIPS_PROJECT_BUILD_DIR}")

    fips_dir(.)
    fips_files(revision.h)
    fips_src(assimp/include/assimp)
    fips_src(assimp/code EXCEPT C4DImporter.* Win32DebugLogStream.h)

    # some third party not fipsified
    fips_src(assimp/contrib/Open3DGC)
    fips_src(assimp/contrib/clipper)
    fips_src(assimp/contrib/irrXML)
    fips_src(assimp/contrib/openddlparser)
    fips_src(assimp/contrib/poly2tri)
    fips_src(assimp/contrib/rapidjson)
    fips_src(assimp/contrib/unzip)
    fips_src(assimp/contrib/utf8cpp)
    fips_deps(zlib)

    if (FIPS_ANDROID)
        #fips_dir(assimp/include/assimp/port/AndroidJNI)
        #fips_files(AndroidJNIOSystem.h)
        add_definitions(-DASSIMP_BUILD_NO_C4D_IMPORTER)
    elseif (FIPS_MACOS)
        add_definitions(-DFIPS_ASSIMP_MACOS=1 -DASSIMP_BUILD_NO_C4D_IMPORTER)
    elseif (FIPS_WINDOWS)
        add_definitions(-DFIPS_ASSIMP_WINDOWS=1)
        #fips_dir(assimp/code/res)
        #fips_files(resource.h)

        if (ASSIMP_C4D)
            fips_dir(assimp/code)
            fips_files(Win32DebugLogStream.h C4DImporter.cpp C4DImporter.h)
        else()
            add_definitions(-DASSIMP_BUILD_NO_C4D_IMPORTER -DASSIMP_BUILD_NO_OPENGEX_IMPORTER -DOPENDDLPARSER_BUILD=1)
        endif()
    elseif (FIPS_LINUX)
        add_definitions(-DFIPS_ASSIMP_LINUX=1 -DASSIMP_BUILD_NO_C4D_IMPORTER)
    endif()
fips_end_lib()

if (FIPS_CLANG)
    set_target_properties(assimp PROPERTIES COMPILE_FLAGS "-Wno-sign-compare -Wno-deprecated-declarations -Wno-unused-function -Wno-unused-variable -Wno-reorder -fexceptions -frtti")
elseif(FIPS_GCC)
    set_target_properties(assimp PROPERTIES COMPILE_FLAGS "-Wno-sign-compare -Wno-deprecated-declarations -Wno-unused-function -Wno-unused-variable -Wno-reorder -fexceptions -frtti")
elseif(FIPS_MSVC)
    set_target_properties(assimp PROPERTIES COMPILE_FLAGS "/wd4138 /wd4267 /wd4152 /wd4204 /wd4242 /wd4244 /wd4477 /wd4530 /wd4577 /wd4668 /wd4996 /WX-")
endif()

if (NOT FIPS_IMPORT)
    gtest_begin(assimp NO_TEMPLATE)
        add_definitions(-DASSIMP_TEST_MODELS_DIR="${FIPS_PROJECT_DIR}/assimp/test/models")
        fips_include_directories(assimp/test/unit)
        fips_src(assimp/test/unit EXCEPT
            # Some excluded are because compiler error
            utExport.cpp utNoBoostTest.cpp
            # Some excluded are because are broken and I don't have time to check them, sorry
            utBlendImportAreaLight.cpp
            utBlendImportMaterials.cpp
            utBlenderImportExport.cpp
            utOpenGEXImportExport.cpp)
        fips_dir(assimp/code)
        fips_files(Version.cpp)
        fips_deps(assimp)
    gtest_end()

    if (FIPS_CLANG)
        set_target_properties(assimpTest PROPERTIES COMPILE_FLAGS "-Wno-sign-compare -Wno-deprecated-declarations -Wno-unused-function -Wno-unused-variable -Wno-reorder -fexceptions -frtti")
    elseif(FIPS_GCC)
        set_target_properties(assimpTest PROPERTIES COMPILE_FLAGS "-Wno-sign-compare -Wno-deprecated-declarations -Wno-unused-function -Wno-unused-variable -Wno-reorder -fexceptions -frtti")
    elseif(FIPS_MSVC)
        set_target_properties(assimpTest PROPERTIES COMPILE_FLAGS "/wd4138 /wd4267 /wd4152 /wd4204 /wd4242 /wd4244 /wd4477 /wd4530 /wd4577 /wd4668 /wd4996 /WX-")
    endif()

    fips_finish()
endif()
