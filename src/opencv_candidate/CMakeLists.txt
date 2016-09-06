# WITH_CXX11
option(WITH_CXX11 "Include -std=c++11options" TRUE)
if(WITH_CXX11)
  include(CheckCXXCompilerFlag)
  CHECK_CXX_COMPILER_FLAG("-std=c++11" COMPILER_SUPPORTS_CXX11)
  if(COMPILER_SUPPORTS_CXX11)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
  else()
    message(STATUS  "The compiler ${CMAKE_CXX_COMPILER} has no C++11 support. Please use a different C++ compiler.")
  endif(COMPILER_SUPPORTS_CXX11)
endif(WITH_CXX11)

add_library(opencv_candidate datamatrix.cpp
                             feature2d.cpp
)

target_link_libraries(opencv_candidate
  ${OpenCV_LIBS}
  )
set_target_properties(opencv_candidate PROPERTIES COMPILE_FLAGS "-fopenmp" LINK_FLAGS "-fopenmp")

#set_target_properties(opencv_candidate PROPERTIES COMPILE_FLAGS "-msse4.2")

install(TARGETS opencv_candidate
    DESTINATION lib
    )
