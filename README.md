# binary-tips-and-tricks

Where we share tips and tricks for fpga/hardware design. Most are 'binary' tricks, please illustrate with a Verilog-like syntax. Whenever possible please provide a link to an example design (does not have to be the design that 'invented it', just an example).

These are usefull tidbits of code we came across looking at designs, or we came up with while optimizing things. This page is to share and remember these cool tricks. Please contribute!

- 1 bit ring for modulo. Declare a register having the size of the modulo `reg [6:0] mod7 = 1`, update by rotation `mod7 <= {mod7[5:0],mod7[6]}`, test if bit 0 is set where needed `wire is_modulo = mod7[0]` (and of course track the bit of your choice to change the initial offset).
Can be seen [here](https://github.com/BrunoLevy/learn-fpga/blob/d836bad382563b953e9ca3510f5f39dcf879bb06/Basic/ULX3S_hdmi/HDMI_test.v#L76).

- 1 bit ring for slower clock, tracking e.g. its raising front. Declare a register having the size of the clock divider `reg [3:0] osc = 1`, update by rotation `osc <= {osc[0,3],osc[3,1]}`, the slower clock is e.g. `clk <= osc[2]|osc[3]` and its posedge is `wire posedge = osc[2]`.
Can be seen [here](https://github.com/sylefeb/Silice/blob/367ae5ca4f4ff7b155ec84c518fa647b8242eb35/projects/ice-v/ice-v.ice#L181)

- Signed wave (eg between [-128,127]) to unsigned wave (eg [0,255]). Flip the sign bit!
Can be seen [here](https://github.com/emard/ulx3s-misc/blob/159edfdb460c3dcdde66138196891dafa5da4f29/examples/audio/hdl/dacpwm.v#L21) and [here](https://github.com/sylefeb/Silice/blob/367ae5ca4f4ff7b155ec84c518fa647b8242eb35/projects/audio_sdcard_streamer/main.ice#L71).

- Counter decreasing, monitoring sign bit.
Can be seen **TODO**

