cmake_minimum_required(VERSION 3.11 FATAL_ERROR)
project(sqlite-gui LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(SOURCES
        src/dialogs.cpp
        src/dialogs.h
        src/global.h
        src/http.cpp
        src/http.h
        src/main.cpp
        src/prefs.cpp
        src/prefs.h
        src/resource.h
        src/resource.rc
        src/tools.cpp
        src/tools.h
        src/utils.cpp
        src/utils.h)

set(SQLITE3_SRC
        include/sqlite3.c
        include/sqlite3.h
        include/sqlite3ext.h)

add_library(sqlite3 ${SQLITE3_SRC})
target_include_directories(sqlite3 PUBLIC "include")
target_compile_definitions(sqlite3 PUBLIC -DSQLITE_ENABLE_COLUMN_METADATA=1)

add_executable(sqlite-gui WIN32 ${SOURCES})
target_include_directories(sqlite-gui PRIVATE "include")
target_compile_definitions(sqlite-gui PRIVATE -D_UNICODE -DUNICODE)
target_link_libraries(sqlite-gui PRIVATE sqlite3 ws2_32.lib gdiplus.lib comctl32.lib wininet.lib msimg32.lib shlwapi.lib)