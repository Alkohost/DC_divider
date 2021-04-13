# DC_divider

T=1/SamplingFrequency;
Rc = 10e6;
R = 1e6;
C = 1e-6;
b = [(Rc+R)*T+2*C*R*Rc, (Rc+R)*T-2*C*R*Rc];
a = [R*T+2*C*R*Rc,      R*T-2*C*R*Rc];
DCreconstructed = filter(b, a, ACsignal); 

For refined method if the parameters cannot be measured directly:
tau= Rc*C; 
k_0=R/(RC+R);
T=1/SamplingFrequency;
b = [T+2*k_0*tau, T-2*k_0*tau];
a = [k_0*T+2*k_0*tau,      k_0*T-2*k_0*tau];
DCreconstructed = filter(b, a, ACsignal);    

Also the filter can be used for online sample-by-sample reconstruction according to the formula:
DCreconst(m)=(b(1)* ACsignal(m)+b(2)* ACsignal(m-1)-a(2)* DCreconst(m-1))/a(1);
