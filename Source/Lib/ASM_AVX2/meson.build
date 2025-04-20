includes = [
    lib_incs,
    include_directories(
        '.',
        '../Codec',
        '../ASM_SSE2',
    ),
]

c_args = [
    '-mavx2',
    '-static-intel',
    '/Qwd10148',
    '/Qwd10010',
    '/Qwd10157',
]
if cc.get_argument_syntax() == 'msvc'
    c_args += '/arch:AVX2'
elif cc.get_id().startswith('intel')
    c_args += '-w'
endif
c_args = cc.get_supported_arguments(c_args)

sources = files(
    'EbCombinedAveragingSAD_Intrinsic_AVX2.c',
    'EbCombinedAveragingSAD_Intrinsic_AVX512.c',
    'EbComputeSAD_Intrinsic_AVX2.c',
    'EbComputeSAD_SadLoopKernel_AVX512.c',
    'EbIntraPrediction_Intrinsic_AVX2.c',
    'EbMCP16bit_Intrinsic_AVX2.c',
    'EbNoiseExtractAVX2.c',
    'EbPackUnPack_Intrinsic_AVX2.c',
    'EbPictureOperators_Intrinsic_AVX2.c',
    'EbTransforms_Intrinsic_AVX2.c',
)

project_libs += static_library('HEVC_ASM_AVX2',
                sources: sources,
                 c_args: c_args,
    include_directories: includes,
                install: false,
)
