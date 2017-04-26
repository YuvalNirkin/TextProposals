# Target
add_executable(img2hierarchy img2hierarchy.cpp)
target_include_directories(img2hierarchy PRIVATE 
	${Boost_INCLUDE_DIRS}
)
target_link_libraries(img2hierarchy PRIVATE
	text_proposal
	${Boost_LIBRARIES}
)

# Installations
install(TARGETS img2hierarchy EXPORT text_proposal-targets DESTINATION bin COMPONENT app)
#install(FILES img2hierarchy.cfg DESTINATION bin COMPONENT app)
