
project('svt-hevc', 'c',
    version: '1.5.1',
    license: [
        'BSD',
        'Patent',
    ],
    license_files: 'LICENSE.md',
    meson_version: '>= 1.1.0',
)

cc = meson.get_compiler('c')

project_name     = meson.project_name()
project_version  = meson.project_version()
project_libs     = []
project_c_args   = []

install_prefix   = get_option('prefix')
install_inc_dir  = join_paths(install_prefix, get_option('includedir'), project_name)
install_lib_dir  = join_paths(install_prefix, get_option('libdir'))
install_bin_dir  = join_paths(install_prefix, get_option('bindir'))
install_data_dir = join_paths(install_prefix, get_option('datadir'), project_name)

if cc.get_argument_syntax() == 'msvc'
    project_c_args += [
        '/MP',
        '/GS',
        '/sdl',
    ]
else
    if host_machine.system() in ['linux', 'gnu']
        project_c_args += '--std=gnu99'
    else
        project_c_args += 'c_std=c99'
    endif
    #for Mingw64 support, see https://gcc.gnu.org/bugzilla/show_bug.cgi?id=65782
    if host_machine.system() == 'windows' and cc.get_define('__MINGW32__') != ''
        project_c_args += '-mxsave'
    endif
    if get_option('NATIVE')
        project_c_args += '-march=native'
    endif
endif

project_c_args = cc.get_supported_arguments(project_c_args)
add_project_arguments(project_c_args, language: 'c')

if host_machine.cpu_family().startswith('x86')
    asm_args = []
    if host_machine.system() == 'windows'
        asm_format = 'win'
    elif host_machine.system() in ['darwin', 'ios', 'tvos']
        asm_format = 'macho'
    else
        asm_format = 'elf'
    endif
    if host_machine.cpu_family() == 'x86_64'
        asm_format += '64'
    else
        asm_format += '32'
    endif

    yasm = find_program('yasm', required: false)
    nasm = find_program('nasm', required: false)
    if nasm.found()
        asm_compiler = nasm
        if host_machine.system() != 'windows'
            asm_args += '-gdwarf'
        endif
        asm_args += [
            '-MQ', '@OUTPUT@',
            '-MF', '@DEPFILE@',
        ]
    elif yasm.found()
        asm_compiler = yasm
        if host_machine.system() != 'windows'
            asm_args += '-gdwarf2'
        endif
    else
        error('nasm or yasm is required')
    endif

    asm_args += [
        '-f', asm_format,
        '@EXTRA_ARGS@',
        '@INPUT@',
        '-o', '@OUTPUT@'
    ]
    foreach asm_inc : ['Source/Lib/ASM_SSE2']
        asm_args += ['-I', '@0@/@1@'.format(meson.current_source_dir(), asm_inc)]
    endforeach

    asm_gen = generator(asm_compiler,
           output: '@BASENAME@.obj',
          depfile: '@BASENAME@.obj.ndep',
        arguments: asm_args)
    #svt_hevc_objs = asm_gen.process(svt_hevc_objs)
endif

subdir('Source/API')
subdir('Source/Lib')
if get_option('BUILD_APP')
    subdir('Source/App')
endif

install_data(
    meson.project_license_files(),
    install_dir: install_data_dir,
)
