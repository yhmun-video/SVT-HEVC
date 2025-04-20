includes = [
    lib_incs,
    include_directories(
        '.',
        '../Codec',
    ),
]

sources = files(
    'EbAvcStyleMcp_C.c',
    'EbComputeMean_C.c',
    'EbComputeSAD_C.c',
    'EbDeblockingFilter_C.c',
    'EbIntraPrediction_C.c',
    'EbMcp_C.c',
    'EbMeSadCalculation_C.c',
    'EbPackUnPack_C.c',
    'EbPictureOperators_C.c',
    'EbSampleAdaptiveOffset_C.c',
    'EbTransforms_C.c',
)

project_libs += static_library('HEVC_C_DEFAULT',
                sources: sources,
    include_directories: includes,
                install: false,
)
