cmake_minimum_required (VERSION 2.8)
project (OpenCV3-beginning)

# find the required packages
find_package(OpenCV REQUIRED)

set(CHAPTERS
    1.beginning
)

set(1.beginning
    1.1.image
    1.2.erode
)

include_directories(${OpenCV_INCLUDE_DIRS})

set(LIBS ${OpenCV_LIBS})

foreach(CHAPTER ${CHAPTERS})
    foreach(DEMO ${${CHAPTER}})
        set(TARGET_DIR ${CMAKE_CURRENT_BINARY_DIR}/bin/${CHAPTER}/${DEMO})
        file(GLOB SOURCE
            "src/${CHAPTER}/${DEMO}/*.h"
            "src/${CHAPTER}/${DEMO}/*.cpp"
        )
        add_executable(${DEMO} ${SOURCE})
        target_link_libraries(${DEMO} ${LIBS}) 
        set_target_properties(${DEMO} PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${TARGET_DIR})
        file(GLOB RESOURCES
            "src/${CHAPTER}/${DEMO}/*.jpg"
            "src/${CHAPTER}/${DEMO}/*.png"
        )
        foreach(RESOURCE ${RESOURCES})
            file(COPY ${RESOURCE} DESTINATION ${TARGET_DIR})
        endforeach(RESOURCE)
    endforeach(DEMO)
endforeach(CHAPTER)
