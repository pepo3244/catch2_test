cmake_minimum_required (VERSION 3.8)

project("catch_test")

enable_testing()


# Visual Studioのフィルタを有効に
set_property(GLOBAL PROPERTY USE_FOLDERS ON)


# C++の設定
enable_language(CXX)
set(CMAKE_CXX_STANDARD 17) # C++17...
set(CMAKE_CXX_STANDARD_REQUIRED ON) #...is required...
set(CMAKE_CXX_EXTENSIONS OFF) #...without compiler extensions like gnu++11


# 警告レベルをあげます
if(MSVC)
	# Force to always compile with W4
	if(CMAKE_CXX_FLAGS MATCHES "/W[0-4]")
		string(REGEX REPLACE "/W[0-4]" "/W4" CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}")
	else()
		set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /W4")
	endif()
elseif(CMAKE_COMPILER_IS_GNUCC OR CMAKE_COMPILER_IS_GNUCXX)
	# Update if necessary
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -Wno-long-long -pedantic")
endif()


# Visual StudioならCRTライブラリを静的リンクするように
if(MSVC)
    string(REPLACE "/MD" "/MT" CMAKE_C_FLAGS_DEBUG            ${CMAKE_C_FLAGS_DEBUG})
    string(REPLACE "/MD" "/MT" CMAKE_C_FLAGS_MINSIZEREL       ${CMAKE_C_FLAGS_MINSIZEREL})
    string(REPLACE "/MD" "/MT" CMAKE_C_FLAGS_RELEASE          ${CMAKE_C_FLAGS_RELEASE})
    string(REPLACE "/MD" "/MT" CMAKE_C_FLAGS_RELWITHDEBINFO   ${CMAKE_C_FLAGS_RELWITHDEBINFO})
    string(REPLACE "/MD" "/MT" CMAKE_CXX_FLAGS_DEBUG          ${CMAKE_CXX_FLAGS_DEBUG})
    string(REPLACE "/MD" "/MT" CMAKE_CXX_FLAGS_MINSIZEREL     ${CMAKE_CXX_FLAGS_MINSIZEREL})
    string(REPLACE "/MD" "/MT" CMAKE_CXX_FLAGS_RELEASE        ${CMAKE_CXX_FLAGS_RELEASE})
    string(REPLACE "/MD" "/MT" CMAKE_CXX_FLAGS_RELWITHDEBINFO ${CMAKE_CXX_FLAGS_RELWITHDEBINFO})
endif(MSVC)


# 追加includeディレクトリ
set(INCLUDE_DIR ${CMAKE_CURRENT_LIST_DIR}/include)
include_directories(${INCLUDE_DIR})


# ライブラリのディレクトリ
set(LIBRARY_DIR_DEBUG ${CMAKE_CURRENT_LIST_DIR}/lib/Debug)
set(LIBRARY_DIR_RELEASE ${CMAKE_CURRENT_LIST_DIR}/lib/Release)


# includeフォルダにあるヘッダーまとめたプロジェクト
file(GLOB_RECURSE catch_test_HEADERS ${INCLUDE_DIR}/*.h ${INCLUDE_DIR}/*.hpp ${INCLUDE_DIR}/*.inl)


# サブプロジェクト
add_subdirectory(src)
add_subdirectory(test)

