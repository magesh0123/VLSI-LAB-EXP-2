![318358593-4a9e2670-3a8d-42fd-a755-f728c5a36b45](https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/f955ff5b-458a-4090-b235-e5d02b6b18c6)![301734849-3cd1f95e-7531-4cad-9154-fdd397ac439e](https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/3800e104-d389-473b-b54e-67f8b3387030)AIM:
To simulate ENCODER, DECODER, MULTIPLEXER, DEMULTIPLEXER, MAGNITUDE COMPARATOR using VIVADO 2023.2.

APPARATUS REQUIRED: 
VIVADO 2023.2

PROCEDURE:
STEP:1  Start  the Xilinx navigator, Select and Name the New project.
STEP:2  Select the device family, device, package and speed.       
STEP:3  Select new source in the New Project and select Verilog Module as the Source type.                       
STEP:4  Type the File Name and Click Next and then finish button. Type the code and save it.
STEP:5  Select the Behavioral Simulation in the Source Window and click the check syntax.                       
STEP:6  Click the simulation to simulate the program and  give the inputs and verify the outputs as per the truth table.               
STEP:7  Select the Implementation in the Sources Window and select the required file in the Processes Window.
STEP:8  Select Check Syntax from the Synthesize  XST Process. Double Click in the  FloorplanArea/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained. 
STEP:9  In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu.
STEP:10 Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here.
STEP:11  On the board, by giving required input, the LEDs starts to glow light, indicating the output.

**LOGIC DIAGRAM**

ENCODER
![301734849-3cd1f95e-7531-4cad-9154-fdd397ac439e](https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/fa882883-2e67-479b-a819-3eac5cb5fead)



DECODE
![301735010-45a5e6cf-bbe0-4fd5-ac84-e5ad4477483b](https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/02726cc5-fca2-4bd1-bbcf-9b3f1eabd2e3)
R



MULTIPLEXER
![301735287-427f75b2-8e67-44b9-ac45-a66651787436](https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/832ec041-3668-4bf7-a1d7-78bb0d72d36f)




DEMULTIPLEXER
![301735386-1c45a7fc-08ac-4f76-87f2-c084e7150557](https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/8eed2415-e7c0-4333-9e62-196da9a19469)



MAGNITUDE COMPARATOR
![301735522-b2fe7a05-6bf7-4dcb-8f5d-28abbf7ea8c2](https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/fcc8fedc-cb20-4e7c-b696-adcdb4dcba3c)


VERILOG CODE
# 3To8Decoder
module decoder(
   input [2:0] a,
   output [7:0] d );
assign d[0]=(~a[2])&(~a[1])&(~a[0]);
assign d[1]=(~a[2])&(~a[1])&(a[0]);
assign d[2]=(~a[2])&(a[1])&(~a[0]);
assign d[3]=(~a[2])&(a[1])&(a[0]);
assign d[4]=(a[2])&(~a[1])&(~a[0]);
assign d[5]=(a[2])&(~a[1])&(a[0]);
assign d[6]=(a[2])&(a[1])&(~a[0]);
assign d[7]=(a[2])&(a[1])&(a[0]);
endmodule


# Demultiplexer 1To8

module demux(din,s,d);
input din;
input[2:0]s;
output [7:0]d;
assign d[0]=(din&~s [2]&~s[1]&~s[0]);
assign d[1]=(din&~s[2]&~s[1]&s[0]);
assign d[2]=(din&~s[2]&s[1]&~s[0]);
assign d[3]=(din&~s[2]&s[1]&s[0]);
assign d[4]=(din&s[2]&~s[1]&~s[0]);
assign d[5]=(din&s[2]&~s[1]&s[0]);
assign d[6]=(din&s[2]&s[1]&~s[0]);
assign d[7]=(din&s[2]&s[1]&s[0]);
endmodule

# Encoder8To3

module encoder_8_to_3(a0,a1,a2,d7,d6,d5,d4,d3,d2,d1,d0);
input d7,d6,d5,d4,d3,d2,d1,d0;
output a0,a1,a2;
or g1(a0,d1,d3,d5,d7);
or g2(a1,d2,d3,d6,d7);
or g3(a2,d4,d5,d6,d7);
endmodule

# Magnitude Compartor

module comparator(a,b,eq,lt,gt);
input [3:0] a,b;
output reg eq,lt,gt;
always @(a,b)
begin
if (a==b)
begin
eq = 1'b1;
lt = 1'b0;
gt = 1'b0;
end
else if (a>b)
begin
eq = 1'b0;
lt = 1'b0;
gt = 1'b1;
end
else
begin
eq = 1'b0;
lt = 1'b1;
gt = 1'b0;
end
end
endmodule

# Multiplexer8To1
module mux(a,s,y);
input [7:0]a;
input [2:0]s;
output y;
reg y;
always@({s ,a})
   begin
      case(s)
         3'b000: y=a[0];
         3'b001: y=a[1];
         3'b010: y=a[2];
         3'b011: y=a[3];
         3'b100: y=a[4];
         3'b101: y=a[5];
         3'b110: y=a[6];
         3'b111: y=a[7];
      endcase
   end
endmodule

OUTPUT WAVEFORM
#  ENCODER
![318353110-a7497d75-f686-43b8-9357-69e59e14eea1](https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/05ec9b4d-9070-4345-932f-b231d15ee1bf)

# DECODER
![318353325-5f78d343-fc3a-4c1e-bfcf-f85bcc58a6e9](https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/9e9cca30-a733-4aa8-a777-f0c742f2c5ba)

 # MULTIPLEXER
![318353752-b5de5822-1f2c-4acd-acb3-1ec962776bfb](https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/2cb4c5bb-4b2d-490a-bede-ae9dd80afa64)

# DEMULTIPLEXER
![318358035-5768add5-fee5-4c52-91c3-e3e3e72aa3ed](https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/bc728cb1-db21-4278-b4eb-cabe9613a993)

# MAGNITUDE COMPARATOR
![318358593-4a9e2670-3a8d-42fd-a755-f728c5a36b45](https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/cbc09a3b-15f2-4a0f-9a5d-eb11c1e57a91)


RESULT
simulation and synthesis ENCODER, DECODER, MULTIPLEXER, DEMULTIPLEXER, MAGNITUDE COMPARATOR using Xilinx ISE is verified.



