includes = [
    lib_incs,
    include_directories(
        '.',
        '../Codec',
    ),
]

c_args = [
    '-msse2',
    '-static-intel',
    '-Wno-attributes',
]
if cc.get_id().startswith('intel')
    c_args += '-w'
endif
c_args = cc.get_supported_arguments(c_args)

sources = files(
    'EbApplySaoLcu16bit_Intrinsic_SSE2.c',
    'EbAvcStyleMcp_Intrinsic_SSE2.c',
    'EbCombinedAveragingSAD_Intrinsic_SSE2.c',
    'EbComputeMean_Intrinsic_SSE2.c',
    'EbDeblockingFilter_Intrinsic_SSE2.c',
    'EbGatherSaoStatistics16bit_Intrinsic_SSE2.c',
    'EbIntraPrediction16bit_Intrinsic_SSE2.c',
    'EbIntraPrediction_Intrinsic_SSE2.c',
    'EbInvTransform_Intrinsic_SSE2.c',
    'EbMcp16bit_Intrinsic_SSE2.c',
    'EbMcp_Intrinsic_SSE2.c',
    'EbMeSadCalculation_Intrinsic_SSE2.c',
    'EbPackUnPack_Intrinsic_SSE2.c',
    'EbPictureOperators_Intrinsic_SSE2.c',
    'EbSaoStatistics_Intrinsic_SSE2.c',
    'EbTransforms_Intrinsic_SSE2.c',
)

objects = []
if host_machine.cpu_family().startswith('x86')
    objects = asm_gen.process([
        'EbGatherSaoStatistics16bit_SSE2.asm',
        'EbPictureOperators_SSE2.asm',
        'x64inc.asm',
        'x64Macro.asm',
        'x64RegisterUtil.asm',
    ])
endif

project_libs += static_library('HEVC_ASM_SSE2',
                objects: objects,
                sources: sources,
                 c_args: c_args,
    include_directories: includes,
                install: false,
)
