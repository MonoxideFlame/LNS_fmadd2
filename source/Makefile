add: PWL.c 
	clang++ -g PWL.c
	./a.out > output.txt

sub: PWL_sub.c 
	clang++ -g PWL_sub.c
	./a.out > output.txt

simulate: add_sub.sv Adder_tb.sv lut.sv S_B.sv
	iverilog -g2012 add_sub.sv Adder_tb.sv lut.sv S_B.sv 
	./a.out

add_sub: add_sub.sv sbdbtb.sv S_B.sv
	iverilog -g2012 add_sub.sv sbdbtb.sv S_B.sv lut.sv
	./a.out

lut_gen: lut_gen.c
	clang -g -lm lut_gen.c
	./a.out

synth: ./verilog/output/add_sub.v Adder_tb.sv standard_cells.v
	iverilog -g2012 ./verilog/output/add_sub.v Adder_tb.sv standard_cells.v
	./a.out
