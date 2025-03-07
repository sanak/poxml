project(poxml)

# search packages used by KDE
#find_package(KDE4 REQUIRED)
find_package(QT4 REQUIRED QtXml)
#include(KDE4Defaults)
#add_definitions (${QT_DEFINITIONS} ${KDE4_DEFINITIONS})
add_definitions (${QT_DEFINITIONS})
#include_directories (${CMAKE_SOURCE_DIR} ${CMAKE_BINARY_DIR} ${KDE4_INCLUDES} ${KDEPIMLIBS_INCLUDE_DIR})
include_directories (${CMAKE_SOURCE_DIR} ${CMAKE_BINARY_DIR} ${QT_INCLUDES})

set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake/modules )
#include(${CMAKE_MODULE_PATH}/KDE4Macros.cmake)
include(${CMAKE_MODULE_PATH}/MacroLogFeature.cmake)
include(${CMAKE_MODULE_PATH}/MacroOptionalFindPackage.cmake)

find_package(GettextPO REQUIRED)
macro_log_feature(GETTEXTPO_FOUND "gettext-po" "A library for processing PO files" "http://www.gnu.org/software/gettext" TRUE "" "Required to build the poxml tools.")

macro_optional_find_package(Gettext)

#add_subdirectory( doc )

include_directories(${GETTEXTPO_INCLUDE_DIR})

########### next target ###############

set(split2po_SRCS split.cpp parser.cpp gettextpoutils.cpp)


#kde4_add_executable(split2po ${split2po_SRCS})
add_executable(split2po ${split2po_SRCS})

target_link_libraries(split2po ${GETTEXTPO_LIBRARY} ${QT_QTXML_LIBRARY} ${QT_QTCORE_LIBRARY})

#install(TARGETS split2po  ${INSTALL_TARGETS_DEFAULT_ARGS})
install(TARGETS split2po RUNTIME DESTINATION "/usr/local/bin")


########### next target ###############

set(xml2pot_SRCS xml2pot.cpp parser.cpp gettextpoutils.cpp)


#kde4_add_executable(xml2pot ${xml2pot_SRCS})
add_executable(xml2pot ${xml2pot_SRCS})

target_link_libraries(xml2pot ${GETTEXTPO_LIBRARY} ${QT_QTXML_LIBRARY} ${QT_QTCORE_LIBRARY})

#install(TARGETS xml2pot  ${INSTALL_TARGETS_DEFAULT_ARGS})
install(TARGETS xml2pot RUNTIME DESTINATION "/usr/local/bin")


########### next target ###############

set(po2xml_SRCS
   po2xml.cpp
   gettextpoutils.cpp
   parser.cpp)


#kde4_add_executable(po2xml ${po2xml_SRCS})
add_executable(po2xml ${po2xml_SRCS})

target_link_libraries(po2xml ${GETTEXTPO_LIBRARY} ${QT_QTXML_LIBRARY} ${QT_QTCORE_LIBRARY})

#install(TARGETS po2xml  ${INSTALL_TARGETS_DEFAULT_ARGS})
install(TARGETS po2xml RUNTIME DESTINATION "/usr/local/bin")

########### next target ###############

set(swappo_SRCS
   swappo.cpp
   gettextpoutils.cpp)


#kde4_add_executable(swappo ${swappo_SRCS})
add_executable(swappo ${swappo_SRCS})

target_link_libraries(swappo ${GETTEXTPO_LIBRARY})

#install(TARGETS swappo  ${INSTALL_TARGETS_DEFAULT_ARGS})
install(TARGETS swappo RUNTIME DESTINATION "/usr/local/bin")



#add_subdirectory(tests)

