add_subdirectory(quickfix)

if( WIN32 OR ${CMAKE_SYSTEM_NAME} STREQUAL "Linux" OR ${CMAKE_SYSTEM_NAME} STREQUAL "Darwin" )

if (QUICKFIX_EXAMPLES)
  add_executable(at at.cpp getopt.c)
  
  target_include_directories(at PRIVATE ${PROJECT_SOURCE_DIR} 
    ${PROJECT_SOURCE_DIR}/src/quickfix ${PROJECT_SOURCE_DIR}/UnitTest++/src)
    
  target_link_libraries(at ${PROJECT_NAME})
endif()

if (QUICKFIX_TESTS)
  add_executable(ut ut.cpp getopt.c ${ut_SOURCES})
  
  target_include_directories(ut PRIVATE ${PROJECT_SOURCE_DIR} 
    ${PROJECT_SOURCE_DIR}/src/quickfix ${PROJECT_SOURCE_DIR}/UnitTest++/src ${PROJECT_SOURCE_DIR}/src/quickfix/test/)
    
  target_link_libraries(ut ${PROJECT_NAME} UnitTest++)
endif()

if (QUICKFIX_EXAMPLES)
  add_executable(pt pt.cpp getopt.c)
  
  target_include_directories(pt PRIVATE ${PROJECT_SOURCE_DIR} 
    ${PROJECT_SOURCE_DIR}/src/quickfix ${PROJECT_SOURCE_DIR}/UnitTest++/src)
    
  target_link_libraries(pt ${PROJECT_NAME})
endif()

endif()

if (HAVE_PYTHON)
add_subdirectory(python)
elseif (HAVE_PYTHON2)
add_subdirectory(python2)
elseif (HAVE_PYTHON3)
add_subdirectory(python3)
endif ()
