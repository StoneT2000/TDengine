CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

PROJECT(TDengine)

INCLUDE_DIRECTORIES(inc ${TD_ROOT_DIR}/src/inc ${TD_OS_DIR}/inc)

IF (TD_LINUX)
  AUX_SOURCE_DIRECTORY(./src SRC)
ELSEIF (TD_DARWIN)
  LIST(APPEND SRC ./src/thaship.c)
  LIST(APPEND SRC ./src/trpc.c)
  LIST(APPEND SRC ./src/tstring.c)
  LIST(APPEND SRC ./src/tudp.c)
ELSEIF (TD_WINDOWS)
  INCLUDE_DIRECTORIES(${TD_ROOT_DIR}/deps/pthread)
  LIST(APPEND SRC ./src/thaship.c)
  LIST(APPEND SRC ./src/trpc.c)
  LIST(APPEND SRC ./src/tstring.c)
  LIST(APPEND SRC ./src/tudp.c)
ENDIF ()

ADD_LIBRARY(trpc ${SRC})
TARGET_LINK_LIBRARIES(trpc tutil)
