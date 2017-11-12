cmake_minimum_required(VERSION 3.5)

project(TissueClassification)

set(MODULE_NAME TissueClassification)

find_package(Slicer REQUIRED)
include(${Slicer_USE_FILE})

SEMMacroBuildCLI(
  NAME ${MODULE_NAME}
  #LOGO_HEADER ${Slicer_SOURCE_DIR}/Resources/ITKLogo.h
  TARGET_LIBRARIES ITKCommon ITKNumerics ITKNrrdIO ITKIO ITKStatistics vtkIO vtkCommon vtkFiltering vtkGraphics vtkRendering
  )

