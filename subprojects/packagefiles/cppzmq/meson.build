project('cppzmq', 'cpp',
  version : '4.10.0',
  license : 'MIT',
  meson_version: '>=0.47.0',
)

libzmq_dep = dependency('libzmq')

cppzmq_dep = declare_dependency(include_directories: include_directories('.'), dependencies: libzmq_dep)

# examples
if get_option('examples')

  ex_pubsub_multithread_inproc_exe = executable('pubsub_multithread_inproc',
    'examples/pubsub_multithread_inproc.cpp',
    dependencies: [cppzmq_dep, dependency('threads')],
    build_by_default: false)

  # don't test pubsub_multithread_inpro, it runs forever
  #test('ex_pubsub_multithread_inpro', ex_pubsub_multithread_inproc_exe)

  ex_hello_world_exe = executable('hello_world',
    'examples/hello_world.cpp',
    dependencies: [cppzmq_dep],
    build_by_default: false)

  test('ex_hello_world', ex_hello_world_exe)

  ex_multipart_messages_exe = executable('multipart_messages',
    'examples/multipart_messages.cpp',
    dependencies: [cppzmq_dep],
    build_by_default: false)

  test('ex_multipart_messages', ex_multipart_messages_exe)

endif

# unit tests
# NOTE: update to v3 in https://github.com/zeromq/cppzmq/pull/632 (enable tests in ci_config.json)
catch2_dep = dependency('catch2', version: '<3.0.0', required: get_option('tests'))
if catch2_dep.found()
  test_src = files([
    'tests/buffer.cpp',
    'tests/message.cpp',
    'tests/context.cpp',
    'tests/socket.cpp',
    'tests/socket_ref.cpp',
    'tests/poller.cpp',
    'tests/active_poller.cpp',
    'tests/multipart.cpp',
    'tests/recv_multipart.cpp',
    'tests/send_multipart.cpp',
    'tests/codec_multipart.cpp',
    'tests/monitor.cpp',
    'tests/utilities.cpp'])
  test_inc = include_directories('tests')

  unit_tests_exe = executable('unit_tests', test_src,
    dependencies: [cppzmq_dep, catch2_dep, dependency('threads')],
    include_directories: [test_inc],
    build_by_default: false)

  test('unit_tests', unit_tests_exe)
endif
