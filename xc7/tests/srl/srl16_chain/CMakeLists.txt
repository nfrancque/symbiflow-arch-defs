add_file_target(FILE basys3_top.v SCANNER_TYPE verilog)
add_file_target(FILE srl16_chain_tb.v SCANNER_TYPE verilog)

add_fpga_target(
  NAME srl16_chain
  BOARD basys3
  INPUT_IO_FILE ../../common/basys3.pcf
  SOURCES basys3_top.v ../common/srl_chain_mixed.v ../common/srl_shift_tester.v ../common/rom.v
  TESTBENCH_SOURCES srl16_chain_tb.v
  EXPLICIT_ADD_FILE_TARGET
  )

add_vivado_target(
  NAME srl16_chain_vivado
  PARENT_NAME srl16_chain
  CLOCK_PINS clk
  CLOCK_PERIODS 10.0
  # TODO: https://github.com/SymbiFlow/symbiflow-arch-defs/issues/1019
  DISABLE_DIFF_TEST
  )

add_dependencies(all_xc7_tests
  testbench_srl16_chain_tb
  testbench_synth_srl16_chain_tb
  testbinch_srl16_chain_tb
)
