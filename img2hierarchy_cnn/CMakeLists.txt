# Target
add_executable(img2hierarchy_cnn img2hierarchy_cnn.cpp)
target_include_directories(img2hierarchy_cnn PRIVATE 
	${Boost_INCLUDE_DIRS}
)
target_link_libraries(img2hierarchy_cnn PRIVATE
	text_proposal
	${Boost_LIBRARIES}
)

# Installations
install(TARGETS img2hierarchy_cnn EXPORT text_proposal-targets DESTINATION bin COMPONENT app)
#install(FILES img2hierarchy_cnn.cfg DESTINATION bin COMPONENT app)
