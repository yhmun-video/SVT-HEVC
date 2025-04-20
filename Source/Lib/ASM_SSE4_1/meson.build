includes = [
    lib_incs,
    include_directories(
        '.',
        '../Codec',
    ),
]

c_args = [
    '-msse4.1',
    '-static-intel',
]
if cc.get_id().startswith('intel')
    c_args += '-w'
endif
c_args = cc.get_supported_arguments(c_args)

sources = files(
    'EbIntraPrediction16bit_Intrinsic_SSE4_1.c',
    'EbPictureOperators_Intrinsic_SSE4_1.c',
    'EbTransforms_Intrinsic_SSE4_1.c',
)

project_libs += static_library('HEVC_ASM_SSE4_1',
                sources: sources,
                 c_args: c_args,
    include_directories: includes,
                install: false,
)
