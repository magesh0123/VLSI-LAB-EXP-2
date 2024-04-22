 # simulation of ENCODER, DECODER, MULTIPLEXER, DEMULTIPLEXER, MAGNITUDE COMPARATOR 
# AIM:
 
     To simulate ENCODER, DECODER, MULTIPLEXER, DEMULTIPLEXER, MAGNITUDE COMPARATOR using VIVADO 2023.1.

# APPARATUS REQUIRED:

                  VIVADO 2023.1

# PROCEDURE:

1. Open Vivado: Launch Xilinx Vivado software on your computer.

2. Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".

3. Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.

4. Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.

5. Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).

6. Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.

7. Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.

8. Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

9. View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.
**LOGIC DIAGRAM**
# ENCODER
![301734849-3cd1f95e-7531-4cad-9154-fdd397ac439e](https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/fa882883-2e67-479b-a819-3eac5cb5fead)
# VERILOG CODE
```
module encoder_8_to_3(a0,a1,a2,d7,d6,d5,d4,d3,d2,d1,d0);
input d7,d6,d5,d4,d3,d2,d1,d0;
output a0,a1,a2;
or g1(a0,d1,d3,d5,d7);
or g2(a1,d2,d3,d6,d7);
or g3(a2,d4,d5,d6,d7);
endmodule
```
# OUTPUT WAVEFORM
![318353110-a7497d75-f686-43b8-9357-69e59e14eea1](https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/05ec9b4d-9070-4345-932f-b231d15ee1bf)

# RTL DESIGN
<img width="764" alt="324391719-08f3ff7c-b9e5-469b-8bb8-53c980cd1ca0" src="https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/54ddc383-ee27-4cfb-b4e4-bcc3e2720b04">

# DECODER
![301735010-45a5e6cf-bbe0-4fd5-ac84-e5ad4477483b](https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/02726cc5-fca2-4bd1-bbcf-9b3f1eabd2e3)

# VERILOG CODE
```
module decoder(input [2:0] a,output [7:0] d );
assign d[0]=(~a[2])&(~a[1])&(~a[0]);
assign d[1]=(~a[2])&(~a[1])&(a[0]);
assign d[2]=(~a[2])&(a[1])&(~a[0]);
assign d[3]=(~a[2])&(a[1])&(a[0]);
assign d[4]=(a[2])&(~a[1])&(~a[0]);
assign d[5]=(a[2])&(~a[1])&(a[0]);
assign d[6]=(a[2])&(a[1])&(~a[0]);
assign d[7]=(a[2])&(a[1])&(a[0]);
endmodule
```
# OUTPUT WAVEFORM
![318353325-5f78d343-fc3a-4c1e-bfcf-f85bcc58a6e9](https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/9e9cca30-a733-4aa8-a777-f0c742f2c5ba)
# RTL DESIGN
<img width="766" alt="324391783-d3549f3d-02f0-47f0-ad57-e5022d165e3b" src="https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/2e4fd12c-b731-49f8-ad9d-370a70d33e8f">


# MULTIPLEXER
![301735287-427f75b2-8e67-44b9-ac45-a66651787436](https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/832ec041-3668-4bf7-a1d7-78bb0d72d36f)

# VERILOG CODE 
```
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
```
# WAVEFORM OUTPUT
![318353752-b5de5822-1f2c-4acd-acb3-1ec962776bfb](https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/2cb4c5bb-4b2d-490a-bede-ae9dd80afa64)

# RTL DESIGN
<img width="761" alt="324391413-85c03dbc-f941-4c48-9ddf-49f4ab5342c4" src="https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/d1c0f5dc-bfb6-4f7a-9eea-ad050207e06c">

# DEMULTIPLEXER
![301735386-1c45a7fc-08ac-4f76-87f2-c084e7150557](https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/8eed2415-e7c0-4333-9e62-196da9a19469)

# VERILOG CODE 
```
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
```

# WAVEFORM OUTPUT
![318358035-5768add5-fee5-4c52-91c3-e3e3e72aa3ed](https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/bc728cb1-db21-4278-b4eb-cabe9613a993)

# RTL DESIGN
<img width="767" alt="324391625-8e681a69-d96e-489a-bea1-b9e273d43b94" src="https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/38db4464-72f1-4155-ae71-93c6773a9a00">

# MAGNITUDE COMPARATOR
![301735522-b2fe7a05-6bf7-4dcb-8f5d-28abbf7ea8c2](https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/fcc8fedc-cb20-4e7c-b696-adcdb4dcba3c)

# VERILOG CODE
```
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
```
# WAVEFORM OUTPUT
![318358593-4a9e2670-3a8d-42fd-a755-f728c5a36b45](https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/cbc09a3b-15f2-4a0f-9a5d-eb11c1e57a91)

# RTL DESIGN
<img width="761" alt="324391559-581f136c-8f0f-40aa-981b-b8299e269f9d" src="https://github.com/magesh0123/VLSI-LAB-EXP-2/assets/162102402/4b937b7a-c5ec-43b3-8f7a-27ca463738b3">

# RESULT
simulation and synthesis ENCODER, DECODER, MULTIPLEXER, DEMULTIPLEXER, MAGNITUDE COMPARATOR using Xilinx ISE is verified.



