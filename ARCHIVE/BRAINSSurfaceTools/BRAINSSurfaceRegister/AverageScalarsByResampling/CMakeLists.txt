StandardBRAINSBuildMacro(NAME AverageScalarsByResampling TARGET_LIBRARIES BRAINSCommonLib ${VTK_LIBRARIES}
  ${BRAINSSurfaceTools_ITK_LIBRARIES})

if (BUILD_TESTING AND NOT BRAINSTools_DISABLE_TESTING)

ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME TEST_SurfaceAverageScalarsByResampling
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:AverageScalarsByResampling>
          --templateSurfaceWithAverageScalars AverageHullOn0036195Test.vtk
          --sphereWithScalarsList DATA{${TestData_DIR}/0036896_left_sphereIC6.vtk}
          --deformedTemplateMeshList DATA{${TestData_DIR}/deformed0036195.vtk}
          --templateSphereFile DATA{${TestData_DIR}/0036195_left_sphere_distToHull.vtk}
          --templateSurfaceFile DATA{${TestData_DIR}/0036195_left_sphere.vtk}
          --numSubs 1 )

ExternalData_add_test( ${BRAINSTools_ExternalData_DATA_MANAGEMENT_TARGET} NAME COMPARE_SurfaceAverageScalarsByResampling
  COMMAND ${LAUNCH_EXE} $<TARGET_FILE:CompareSurfaces>
          --inputSurfaceFile AverageHullOn0036195Test.vtk
          --refSurfaceFile DATA{${TestData_DIR}/AverageHullOn0036195.vtk}
          --vertexLocation
          --scalarArray
          --tolerance 1.0e-7 )

set_tests_properties( COMPARE_SurfaceAverageScalarsByResampling PROPERTIES DEPENDS TEST_SurfaceAverageScalarsByResampling )

endif ()
