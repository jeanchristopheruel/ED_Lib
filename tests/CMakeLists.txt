find_package(OpenCV 4.0 REQUIRED core imgproc imgcodecs)

add_executable(test test.cpp)
target_link_libraries(test ${OpenCV_LIBS} EDLib)
target_include_directories(test PUBLIC ${OpenCV_INCLUDE_DIRS})

add_executable(test_ED test_ED.cpp)
target_link_libraries(test_ED ${OpenCV_LIBS} EDLib)
target_include_directories(test_ED PUBLIC ${OpenCV_INCLUDE_DIRS})

add_executable(video_test video_test.cpp)
target_link_libraries(video_test ${OpenCV_LIBS} EDLib)
target_include_directories(video_test PUBLIC ${OpenCV_INCLUDE_DIRS})