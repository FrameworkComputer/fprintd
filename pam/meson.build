mapfile = files('pam_fprintd.ver')
pam_modules_dir = get_option('pam_modules_dir')
if pam_modules_dir == ''
    pam_modules_dir = '/' / get_option('libdir') / 'security'
endif

pam_fprintd = shared_module('pam_fprintd',
    name_prefix: '',
    include_directories: [
        include_directories('..'),
    ],
    sources: [
        'pam_fprintd.c',
        'fingerprint-strings.h',
    ],
    dependencies: [
        libsystemd_dep,
        pam_dep,
        gettext_deps,
    ],
    c_args: [
        '-DLOCALEDIR="@0@"'.format(localedir),
    ] + (libsystemd_dep.name() == 'basu' ? ['-DFPRINTD_PAM_USE_BASU'] : []),
    link_args: [
        '-Wl,--version-script,@0@/@1@'.format(meson.source_root(), mapfile[0]),
        '-Wl,--unresolved-symbols=report-all',
    ],
    link_depends: mapfile,
    install: true,
    install_dir: pam_modules_dir,
)
