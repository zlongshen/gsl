cmake_minimum_required (VERSION 2.6)
project (gsl)
set(TEST_FILE "log.txt")
add_custom_command(OUTPUT  ${TEST_FILE}
  COMMAND echo "Generating log.txt file..."
  COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_CURRENT_LIST_FILE} ${TEST_FILE}
  COMMENT  "This is a test"
 )
add_custom_target(Test1 ALL DEPENDS ${TEST_FILE})


add_custom_command(TARGET Test1
  PRE_BUILD
  COMMAND echo "executing a fake command"
  COMMAND echo `pwd`
  COMMAND cd ${PROJECT_SOURCE_DIR}/src && make && sudo make install
  COMMENT "This command will be executed before building target Test1"
 )