```VHDL
// 256 x 3 memory module with one read/write port
module dmem( input logic clk, we,
		input logic[7:0] a
		input logic [2:0] wd,
		output logic [2:0] rd);
	logic [2:0] RAM[255:0];
	assign rd = RAM[a];
	always @(posedge clk)
	if (we)
	RAM[a] <= wd;
endmodule
```