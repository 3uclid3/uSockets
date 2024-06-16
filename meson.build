project('uSockets', ['c', 'cpp'])

c_args = ''
cpp_args = ''
ld_args = ''

sources = files(
    'src/bsd.c',
    'src/context.c',
    'src/crypto/openssl.c',
    'src/eventing/epoll_kqueue.c',
    'src/eventing/gcd.c',
    'src/eventing/libuv.c',
    'src/io_uring/io_context.c',
    'src/io_uring/io_loop.c',
    'src/io_uring/io_socket.c',
    'src/loop.c',
    'src/quic.c',
    'src/socket.c',
    'src/udp.c',
)

if get_option('openssl')
    c_args += '-DLIBUS_USE_OPENSSL'
endif

if get_option('libuv')
    c_args += '-DLIBUSE_USE_LIBUV'
    ld_args += '-luv'
endif

if not get_option('openssl') and not get_option('boringssl')
    c_args += '-DLIBUS_NO_SSL'
endif

deps = [dependency('zlib')]

usockets = static_library(
    'uSockets',
    sources,
    c_args: [c_args],
    cpp_args: [cpp_args],
    link_args: [ld_args],
    build_by_default: true,
    include_directories: ['src'],
    dependencies: deps,

)

usockets_dep = declare_dependency(
    link_with: usockets,
    include_directories: ['src'],
    dependencies: deps,
)