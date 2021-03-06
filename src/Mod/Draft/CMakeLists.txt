add_subdirectory(App)

IF (BUILD_GUI)
    PYSIDE_WRAP_RC(Draft_QRC_SRCS Resources/Draft.qrc)
ENDIF (BUILD_GUI)

SET(Draft_SRCS
    Init.py
    InitGui.py
    Draft.py
    DraftTools.py
    DraftGui.py
    DraftSnap.py
    DraftTrackers.py
    DraftVecUtils.py
    DraftGeomUtils.py
    WorkingPlane.py
    importDXF.py
    importOCA.py
    importSVG.py
    importDWG.py
    importAirfoilDAT.py
    TestDraft.py
)
SOURCE_GROUP("" FILES ${Draft_SRCS})

ADD_CUSTOM_TARGET(Draft ALL
    SOURCES ${Draft_SRCS} ${Draft_QRC_SRCS}
)

fc_copy_sources(Draft "${CMAKE_BINARY_DIR}/Mod/Draft" ${Draft_SRCS})

IF (BUILD_GUI)
    fc_target_copy_resource(Draft
        ${CMAKE_CURRENT_BINARY_DIR}
        ${CMAKE_BINARY_DIR}/Mod/Draft
        Draft_rc.py)
ENDIF (BUILD_GUI)

INSTALL(
    FILES
        ${Draft_SRCS}
        ${Draft_QRC_SRCS}
    DESTINATION
        Mod/Draft
)
