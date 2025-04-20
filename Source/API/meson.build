headers = files(
    'EbApi.h',
    'EbErrorCodes.h',
)

versions = project_version.split('.')
ver_data = configuration_data()
ver_data.set('SVT_HEVC_VERSION_MAJOR'     , versions[0])
ver_data.set('SVT_HEVC_VERSION_MINOR'     , versions[1])
ver_data.set('SVT_HEVC_VERSION_PATCHLEVEL', versions[2])
headers += configure_file(
    configuration: ver_data,
            input: 'EbApiVersion.h.in',
           output: 'EbApiVersion.h',
)

install_headers(headers,
    install_dir: install_inc_dir
)

lib_incs = include_directories('.')
