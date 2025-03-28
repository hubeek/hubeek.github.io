# OCP Chapter 11

_Status: Published_
_Created: 2024-07-30 16:45:11_
_Tags: ocp_

# Modules

### Custom Java Builds
jlink used to create runtime images.  

### Improved performance
### unique package enforcement
- anders twee packages met zelfde naam maar verschillende code

## Creating and Running a Modular program
- code files nofidig
- module-info.java file  nodig
- module-info.java file can be empty
- (weetje ) zelfs empty .java class kan in project. De compiler skipt m dan
- javac  optie -d specifies de dir in which t compiles
- javac optie --module-path indicates location of custom module files
- javac optie -p is gelijk aan --module-path

javac -d <dir>  

javac -p <path> is gleijk aan javac --module-path  




### Module-info file operators

- exports
- requires
- provides
- uses
- opens

#### Exports
- possible to exports to specific module. `exports a.b.c to a.d`
- access control via private, default (package-private), protected, public

### Requires transitive
- requires *modeulName* specifies that the current module depends on *moduleName*
- **requires transitive** specifies  any module that requires this module will also depend on *moduleName*
- `requires` and `requires transitive` met dezelfde ref  mogen niet samen in module-info

### provides, uses, opens
- hoef je alleen te weten dat ze bestaan
- provides specifies that a class provides an implementation of a service (zoals een interface...)
- uses specifies that a module is relying on a service. 
- opens is voor runtime inspection... moet apart worden opgegeven ivm security




## java Command
3 module related options:
- describing with --describe-module (vermeld dan ook java.base module)
- listing --list-modules
- module resolution --show-module-resolution

## jar Command
- `--file` of `-f` beschrijf module (feitelijk hetzelfde als java --describe-module)

## jdeps Command
- info about dependencies within the module.
- jdeps -s of jdeps -summary (maar 1 minnetje...)
- kan ook zonder -s of -summary
- `--module-path` kan niet worden afgekort in jdeps.... maar moet je helemaal uitschrijven...

## jmods Command
- jmod is only working with jmod files


[prev](http://hjh.devsnips.nl/ocp10)
[next](http://hjh.devsnips.nl/ocp12)