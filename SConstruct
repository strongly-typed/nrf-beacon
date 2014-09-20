# path to the xpcc root directory
rootpath = 'xpcc'

env = Environment(tools = ['xpcc'], toolpath = [rootpath + '/scons/site_tools'])

# find all source files
files = env.FindFiles('src')

# build the program
program = env.Program(target = env['XPCC_CONFIG']['general']['name'], source = files.sources)

# build the xpcc library
env.XpccLibrary()

# create a file called 'defines.hpp' with all preprocessor defines if necessary
env.Defines()

env.Alias('size', env.Size(program))
env.Alias('symbols', env.Symbols(program))
env.Alias('defines', env.ShowDefines())

hexfile = env.Hex(program)
binfile = env.Bin(program)

env.Alias('dfu', env.DfuStm32Programmer(binfile))
env.Alias('program', env.OpenOcd(program))
env.Alias('build', [hexfile, env.Listing(program)])
env.Alias('all', ['build', 'size'])

env.Default('all')
