cmake_minimum_required (VERSION 3.8)

include("contrib/Catch.cmake")
include("contrib/ParseAndAddCatchTests.cmake")

# ソースをこのプロジェクトの実行可能ファイルに追加します。
add_executable(catch_test_test)

target_sources(catch_test_test PRIVATE 
	${CMAKE_CURRENT_LIST_DIR}/Source/main.cpp
)

target_include_directories(catch_test_test PRIVATE "catch")

# add_test(
# 	NAME catch_test_test
# 	COMMAND $<TARGET_FILE:catch_test_test>
# )
catch_discover_tests(catch_test_test)
#ParseAndAddCatchTests(catch_test_test)

# # Visual Studioのフィルタの設定
# get_target_property(catch_test_Files catch_test SOURCES)
# source_group(TREE "${CMAKE_CURRENT_LIST_DIR}/Source" PREFIX "\\Source" FILES ${catch_test_Files})

# # ついでにincludeディレクトリも表示されるように
# target_sources(catch_test PRIVATE ${catch_test_HEADERS})
# source_group(TREE "${INCLUDE_DIR}" PREFIX "\\include" FILES ${catch_test_HEADERS})

