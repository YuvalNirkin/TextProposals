# Source
file(GLOB HDR "*.h")
file(GLOB SRC "*.cpp")

# Target
add_library(text_proposal ${SRC} ${HDR})
target_include_directories(text_proposal PUBLIC
	$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
	$<BUILD_INTERFACE:${CMAKE_CURRENT_BINARY_DIR}>
	${OpenCV_INCLUDE_DIRS}
	${Caffe_INCLUDE_DIRS}
	${PROTOBUF_INCLUDE_DIRS}
)
target_link_libraries(text_proposal PUBLIC
	${OpenCV_LIBS}
	${Caffe_LIBRARIES}
	${PROTOBUF_LIBRARIES}
)

# Installations
install(TARGETS text_proposal
	 EXPORT text_proposal-targets
     RUNTIME DESTINATION bin COMPONENT dev
     LIBRARY DESTINATION lib COMPONENT dev
     ARCHIVE DESTINATION lib COMPONENT dev)
install(FILES ${HDR} DESTINATION include)
