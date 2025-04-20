includes = [
    lib_incs,
    include_directories(
        '.',
        '../Codec',
    ),
]

c_args = [
    '-mssse3',
    '-static-intel',
]
if cc.get_id().startswith('intel')
    c_args += '-w'
endif
c_args = cc.get_supported_arguments(c_args)

sources = files(
    'EbAvcStyleMcp_Intrinsic_SSSE3.c',
    'EbDeblockingFilter16bit_Intrinsic_SSSE3.c',
    'EbDeblockingFilter_Intrinsic_SSSE3.c',
    'EbIntraPrediction16bit_Intrinsic_SSSE3.c',
    'EbMcp_Intrinsic_SSSE3.c',
    'EbSaoApplication_Intrinsic_SSSE3.c',
    'EbTransforms_Intrinsic_SSSE3.c',
)

project_libs += static_library('HEVC_ASM_SSSE3',
                sources: sources,
                 c_args: c_args,
    include_directories: includes,
                install: false,
)
