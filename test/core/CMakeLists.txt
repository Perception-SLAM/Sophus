# Ensure that ${Sophus_INCLUDE_DIR} is first on search path
INCLUDE_DIRECTORIES( BEFORE ${Sophus_INCLUDE_DIR} )

# Tests to run
SET( TEST_SOURCES test_so2 test_se2 test_so3 test_se3 test_rxso3 test_sim3)

# git clone https://ceres-solver.googlesource.com/ceres-solver
find_package( Ceres 1.6.0 QUIET )

if( Ceres_FOUND )
    # Ensure that ${Sophus_INCLUDE_DIR} is first on search path
    INCLUDE_DIRECTORIES( BEFORE ${Sophus_INCLUDE_DIR} ${CERES_INCLUDES})
    add_definitions(-DSOPHUS_CERES_FOUND)
endif()

FOREACH(test_src ${TEST_SOURCES})
  ADD_EXECUTABLE( ${test_src} ${test_src}.cpp tests.hpp)
  ADD_TEST( ${test_src} ${test_src} )
ENDFOREACH(test_src)
