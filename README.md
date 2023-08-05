# Sequence-Detector
In this project, I designed an FSM, to detect 1101 sequence. For this, we programmed in verilog, using Behavioural Modellng Style. The code for sequence detector-1101 is as follows:-

//sequence detector for 1101
module FSM_1101(
input x, 
input clk, 
input rst, 
output reg z);
parameter S0=0, S1=1,S11=2, S110=3;

reg [1:0] state;

always@(posedge clk) begin
    if(rst == 1'b1) begin
        z <= 0;
        state <= S0;
    end
    else  begin
        case(state)
        S0: begin
            state <= x ? S1: S0;
            z <= 0;
        end
        S1: begin
            state <= x ? S11 : S0;
            z <= 0;
        end
        S11 : begin
            state <= x ? S11 : S110;
            z <= 0;
        end
        S110 : begin
            state <= x ? S1:S0;
            z = x ? 1 : 0;
        end
        default : begin
            state <= S0;
            z <= 0;
        end
        endcase
    end   
end
endmodule

In order to detect 1101, we created 4 states. State-1(S0) was the stage where no bit from 1101 is detected. Then, once we detect 1st bit of 1101 i.e '1', we get to Stage-
2(S1) After which, we look for another '1' for the next(2nd) bit. Once we have detected another '1' we get to Stage-3(S11). Or if we receive a 0, we are back to Stage-
1(S0). Now, on Stage-3, we look for 3rd bit(0). If we get '0', we get to Stage-4(S110). While, If we receive a '1', we remain at Stage-3(S11). Now, we are only left with 
the last bit(1). So, if we receive a '1', we have detected the whole sequence and we'll repeat the whole step again. While, if we get a '0', we getback to Stage-1(S0).

Deducing this, we can make state table & state diagram for the same.
