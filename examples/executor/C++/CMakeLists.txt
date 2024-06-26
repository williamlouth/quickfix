if (HAVE_SSL AND WIN32)
set(applink_SOURCE ${OPENSSL_INCLUDE_DIR}/openssl/applink.c)
endif()

set (executor_NAME executor)
if (WIN32)
set (executor_NAME ${executor_NAME}_cpp)
endif()

add_executable(${executor_NAME} Application.cpp executor.cpp ${applink_SOURCE})

target_include_directories(${executor_NAME} PRIVATE ${PROJECT_SOURCE_DIR}/include ${PROJECT_SOURCE_DIR}/include/quickfix ${PROJECT_SOURCE_DIR})

target_link_libraries(${executor_NAME} ${PROJECT_NAME})

if (NOT WIN32)
ADD_CUSTOM_TARGET(${executor_NAME}_target ALL
                  COMMAND ${CMAKE_COMMAND} -E create_symlink $<TARGET_FILE:executor> ${PROJECT_SOURCE_DIR}/bin/${executor_NAME})
else()
set_target_properties(${executor_NAME} PROPERTIES
                      RUNTIME_OUTPUT_DIRECTORY_DEBUG ${PROJECT_SOURCE_DIR}/bin/debug/executor_cpp/
                      RUNTIME_OUTPUT_DIRECTORY_RELEASE ${PROJECT_SOURCE_DIR}/bin/release/executor_cpp/
                      RUNTIME_OUTPUT_DIRECTORY_RELWITHDEBINFO ${PROJECT_SOURCE_DIR}/bin/release/executor_cpp/)
endif()

