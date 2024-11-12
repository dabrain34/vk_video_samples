# Define a custom target to generate the dispatch table files
add_custom_target(GenerateDispatchTables
    DEPENDS ${VK_VIDEO_COMMON_LIBS_SOURCE_ROOT}/VkCodecUtils/HelpersDispatchTable.h
            ${VK_VIDEO_COMMON_LIBS_SOURCE_ROOT}/VkCodecUtils/HelpersDispatchTable.cpp
)

# Add the custom command to generate the dispatch tables
macro(generate_dispatch_table out)
    add_custom_command(OUTPUT ${out}
        COMMAND ${PYTHON_EXECUTABLE} ${SCRIPTS_DIR}/generate-dispatch-table.py ${out}
        DEPENDS ${SCRIPTS_DIR}/generate-dispatch-table.py
        )
endmacro()

generate_dispatch_table(${VK_VIDEO_COMMON_LIBS_SOURCE_ROOT}/VkCodecUtils/HelpersDispatchTable.h)
generate_dispatch_table(${VK_VIDEO_COMMON_LIBS_SOURCE_ROOT}/VkCodecUtils/HelpersDispatchTable.cpp)


set (helpers_dispatch_table_gen
    ${VK_VIDEO_COMMON_LIBS_SOURCE_ROOT}/VkCodecUtils/HelpersDispatchTable.cpp
    ${VK_VIDEO_COMMON_LIBS_SOURCE_ROOT}/VkCodecUtils/HelpersDispatchTable.h
)

# Create a static library from the generated file
add_library(HelpersDispatchTableGen STATIC ${helpers_dispatch_table_gen})