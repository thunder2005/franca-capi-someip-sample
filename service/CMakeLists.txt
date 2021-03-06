project(MLService)

set(COMMONAPI_PATH ${COMMONAPI})
set(FIDL_PATH ${FIDL})

set(CMAKE_MODULE_PATH ${MODULES_PATH})
include(IpcMacro)

add_capi_types(MLStub com.ford.rnd.MLTypes:1)
add_capi_interfaces(MLStub com.ford.rnd.ML:1 com.ford.rnd.SmartML:1)
add_capi_library(MLStub)

add_capi_interfaces(ButtonsStub com.ford.rnd.Buttons:1)
add_capi_library(ButtonsStub)

set(SOURCE
  service.cpp
  mlservice.cpp
  smartmlservice.cpp
  buttonsservice.cpp
)

add_executable(${PROJECT_NAME} ${SOURCE})
target_link_libraries(${PROJECT_NAME} CommonAPI MLStub ButtonsStub)

install(TARGETS ${PROJECT_NAME}
  RUNTIME DESTINATION ${CMAKE_BINARY_DIR}/build/bin
  LIBRARY DESTINATION ${CMAKE_BINARY_DIR}/build/lib
  PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE
)
