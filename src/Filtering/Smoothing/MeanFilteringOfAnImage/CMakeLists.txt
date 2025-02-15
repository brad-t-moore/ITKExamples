cmake_minimum_required(VERSION 3.10.2)

project( MeanFilteringOfAnImage )

find_package( ITK REQUIRED )
include( ${ITK_USE_FILE} )

add_executable( MeanFilteringOfAnImage Code.cxx )
target_link_libraries( MeanFilteringOfAnImage ${ITK_LIBRARIES} )

install( TARGETS MeanFilteringOfAnImage
  DESTINATION bin/ITKExamples/Filtering/Smoothing
  COMPONENT Runtime
)

install( FILES Code.cxx CMakeLists.txt
  DESTINATION share/ITKExamples/Code/Filtering/Smoothing/MeanFilteringOfAnImage
  COMPONENT Code
)

enable_testing()
add_test( NAME MeanFilteringOfAnImageTest
  COMMAND ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/MeanFilteringOfAnImage
    ${CMAKE_CURRENT_BINARY_DIR}/Gourds.png
    Output.png
    2
  )

if( ITK_WRAP_PYTHON )
  add_test( NAME MeanFilteringOfAnImageTestPython
    COMMAND ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/Code.py
      ${CMAKE_CURRENT_BINARY_DIR}/Gourds.png
      OutputPython.png
      2
    )
endif()
