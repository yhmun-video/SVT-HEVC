

sources = files(
    'EbAppConfig.c',
    'EbAppContext.c',
    'EbAppString.c',
    'EbAppMain.c',
    'EbAppProcessCmd.c',
    'EbTime.c',
    'EbAppInputy4m.c',
)

includes = [
    lib_incs,
    include_directories('.'),
]

executable('SvtHevcEncApp',
                sources: sources,
    include_directories: includes,
           dependencies: svt_hevc_dep,
            install_dir: install_bin_dir,
                install: true,
)
