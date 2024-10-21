# 添加项目 "ImGui"
add_library(ImGui STATIC
    imconfig.h
    imgui.h
    imgui_internal.h
    imstb_rectpack.h
    imstb_textedit.h
    imstb_truetype.h
    imgui.cpp
    imgui_demo.cpp
    imgui_draw.cpp
    imgui_tables.cpp
    imgui_widgets.cpp
)

# 设置编程语言和标准
set_target_properties(ImGui PROPERTIES
    LANGUAGE CXX
    CXX_STANDARD 17
    ARCHIVE_OUTPUT_DIRECTORY "${OUTPUT_DIR}/ImGui"
    OBJECT_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin-int/${OUTPUT_DIR}/ImGui"
)

# Windows 特定设置
if (WIN32)
    target_compile_definitions(ImGui PRIVATE
        WIN32_LEAN_AND_MEAN  # 推荐的 Windows 定义
    )
    target_compile_options(ImGui PRIVATE
        /MT  # 使用静态运行时
    )
endif()

# 调整构建选项
if (CMAKE_BUILD_TYPE MATCHES "Debug")
    target_compile_options(ImGui PRIVATE
        /MTd  # Debug 模式下的静态运行时
    )
elseif (CMAKE_BUILD_TYPE MATCHES "Release")
    target_compile_options(ImGui PRIVATE
        /MT  # Release 模式下的静态运行时
    )
endif()
