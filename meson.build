project(
  'nemora-postd',
  'cpp',
  version: '0.1', meson_version: '>=0.49.0',
  default_options: [
    'warning_level=3',
    'werror=true',
    'cpp_std=c++17'
  ],
)

protobuf = dependency('protobuf')
phosphor_dbus_interfaces = dependency('phosphor-dbus-interfaces')
sdbusplus = dependency('sdbusplus')
threads = dependency('threads')
logging = dependency('phosphor-logging')
fmt = declare_dependency(compile_args: '-DFMT_STRING_ALIAS=1', dependencies: dependency('fmt'))

protoc = find_program('protoc', native: true)

gen = generator(protoc, \
  output: ['@BASENAME@.pb.cc', '@BASENAME@.pb.h'],
  arguments : ['--proto_path=@SOURCE_DIR@', '--cpp_out=@BUILD_DIR@', '@INPUT@'],
)

generated = gen.process(['event_message.proto'])

executable(
  'nemora-postd',
  'nemorad.cpp',
  'src/host_manager.cpp',
  'src/nemora.cpp',
  'src/socket_manager.cpp',
  'src/serializer.cpp',
  generated,
  include_directories: include_directories('.'),
  dependencies: [protobuf, phosphor_dbus_interfaces, sdbusplus, threads, logging, fmt],
  install: true
)


