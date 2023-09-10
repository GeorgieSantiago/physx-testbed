import os
import scons_compiledb

env = Environment()

scons_compiledb.enable(env)

physx_libpath = os.path.abspath('../physx/physx/bin/win.x86_64.vc143.mt/debug/')
print(physx_libpath)
physx_libs = ['PhysX_64', 'PhysXCommon_64', 'PhysXFoundation_64', 'PhysXCooking_64', 'PhysXExtensions_static_64', 'PhysXPvdSDK_static_64']

def get_prefixed_director(prefix, excluded = []) -> list:
    return [f"{prefix}/{filename}/" for filename in os.listdir(prefix) if os.path.isdir(os.path.join(prefix,filename)) and filename not in excluded]

def configure_physx():
    physx_includes: list = get_prefixed_director( "../physx/physx/include")
    env.Append(CPPPATH=['../physx/physx/include/'])
    env.Append(CPPPATH=physx_includes)
    env.Append(CPPPATH=['../physx/pxshared/include/'])
    env.Append(CCFLAGS=['/MTd'])
    # env.Append(CXXFLAGS = ['/MT'])
    env.Append(LIBPATH=[physx_libpath])
    env.Append(LIBS=physx_libs)

configure_physx()

env.Program('physx-testbed', Glob('./*.cpp'))

env.CompileDb()