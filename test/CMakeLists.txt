#
#
# Compiling/running tests

set ( CMAKE_RUNTIME_OUTPUT_DIRECTORY ${dist_dir}/test )

# NOT ctest.h
set (crusty_files test_utils.c test_utils.h)

macro (ls_test name)
  add_executable ( ${name}_test ${name}_test.c test_utils.c )
  target_link_libraries ( ${name}_test PRIVATE ls)
  target_include_directories ( ${name}_test PRIVATE ../include )
  add_test ( NAME ${name} COMMAND ${name}_test )
  list(APPEND crusty_files ${name}_test.c)
endmacro()

ls_test ( ls_error )
ls_test ( ls_eventing )
ls_test ( ls_htable )
ls_test ( ls_log )
ls_test ( ls_mem )
ls_test ( ls_pktinfo )
ls_test ( ls_queue )
ls_test ( ls_sockaddr )
ls_test ( ls_str )
ls_test ( ls_timer )

include ( CTest )
UncrustifyDir(crusty_files)
