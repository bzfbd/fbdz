set(LLVM_TARGET_DEFINITIONS Options.td)
tablegen(LLVM Options.inc -gen-opt-parser-defs)
add_public_tablegen_target(ELFOptionsTableGen)

add_lld_library(lldELF
  Driver.cpp
  DriverUtils.cpp
  EhFrame.cpp
  Error.cpp
  ICF.cpp
  InputFiles.cpp
  InputSection.cpp
  LTO.cpp
  LinkerScript.cpp
  MarkLive.cpp
  OutputSections.cpp
  Relocations.cpp
  ScriptParser.cpp
  Strings.cpp
  SymbolListFile.cpp
  SymbolTable.cpp
  Symbols.cpp
  Target.cpp
  Thunks.cpp
  Writer.cpp

  LINK_COMPONENTS
  ${LLVM_TARGETS_TO_BUILD}
  Analysis
  BitReader
  BitWriter
  Codegen
  Core
  IPO
  Linker
  LTO
  Object
  Option
  Passes
  MC
  Support
  Target
  TransformUtils

  LINK_LIBS
  lldConfig
  ${PTHREAD_LIB}
  )

add_dependencies(lldELF intrinsics_gen ELFOptionsTableGen)
