add_file_target(FILE basys3_top.v SCANNER_TYPE verilog)
add_file_target(FILE srl32_init_tb.v SCANNER_TYPE verilog)

add_fpga_target(
  NAME srl32_init
  BOARD basys3
  INPUT_IO_FILE ../../common/basys3.pcf
  SOURCES basys3_top.v ../common/srl_init_tester.v ../common/rom.v
  TESTBENCH_SOURCES srl32_init_tb.v
  EXPLICIT_ADD_FILE_TARGET
  )

add_vivado_target(
  NAME srl32_init_vivado
  PARENT_NAME srl32_init
  CLOCK_PINS clk
  CLOCK_PERIODS 10.0
  )

add_dependencies(all_xc7_tests
  testbench_srl32_init_tb
  testbench_synth_srl32_init_tb
  testbinch_srl32_init_tb
)
