project(TissueClassification)

cmake_minimum_required(VERSION 2.4)

if(COMMAND cmake_policy)
  cmake_policy(SET CMP0003 NEW)
endif(COMMAND cmake_policy)

include_directories( ${SlicerBaseCLI_BINARY_DIR} ${SlicerBaseCLI_SOURCE_DIR} )

link_directories(${ModuleDescriptionParser_BINARY_DIR})
link_directories(${SlicerBaseCLI_BINARY_DIR})

find_package(Slicer3 REQUIRED NO_DEFAULT_PATH)

if (Slicer3_FOUND)
  include(${Slicer3_USE_FILE})
  slicer3_set_default_install_prefix_for_external_projects()

  set (CLP TissueClassification)

  add_library(${CLP}Lib SHARED ${CLP}.cxx)
  set_target_properties (${CLP}Lib PROPERTIES COMPILE_FLAGS "-Dmain=ModuleEntryPoint")
  slicer3_set_plugins_output_path(${CLP}Lib)
  target_link_libraries (${CLP}Lib ITKCommon ITKNumerics ITKNrrdIO ITKIO ITKStatistics vtkIO vtkCommon vtkFiltering vtkGraphics vtkRendering)

  set ( ${CLP}_SOURCE ${CLP}.cxx)
  generateclp(${CLP}_SOURCE ${CLP}.xml)
  add_executable(${CLP} ${${CLP}_SOURCE})
  target_link_libraries (${CLP} ${CLP}Lib)

  slicer3_set_plugins_output_path(TissueClassification)
  slicer3_install_plugins(TissueClassification)

  add_subdirectory(Testing)

else (Slicer3_FOUND)

message(WARNING "Cannot build with a Slicer3 build tree or a Slicer3 installation. Please set Slicer3_DIR. If using a Slicer3 build, Slicer3_DIR needs to be set to the root of the build tree of Slicer3.  If using an installation of Slicer3, Slicer3_DIR needs to be set to <SlicerInstallation>/lib/Slicer3.")

endif (Slicer3_FOUND)

################################################

