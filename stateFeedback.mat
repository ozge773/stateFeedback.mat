%%State feedback example from lessons#25_1 %%

%Example static feedback controller
clear all 
close all
clc
format compact

A = [-0.1 -1;1 0]
B = [1;0]
C = [0 1]
D = 0 
x0 = [0;0] % inital condition 

%Cecking the reachability  


M_r = ctrb(A,B)
rho_M = rank(M_r)
rho = 1

%damping coff
%natura lfreq
%settling time
% those values is used to compute the eigenvalues in cartesian form 
%max overshoot


s_hat = 0.10 %maximum overshoot requirement 
t_s2 = 6.5 %settling time 2% requirement
zeta = abs(log(s_hat)) / sqrt(pi^2 +(log(s_hat))^2) %zeta value is in the formula sheet
wn = log((2/100)^(-1))/(zeta*t_s2)%log((2/100)^(-1))/(zeta*t_s2) if you write this version it is wrong
lambda1 = -zeta *wn + j*wn*sqrt(1-zeta^2)
lambda2 = -zeta *wn - j*wn*sqrt(1-zeta^2)
lamda_des = [lambda1 lambda2]
K = place(A,B, lamda_des)


A_c = A-B*K %in the steady state design formula sheet
B_c =B
C_c = C
D_c = 0

sys_c = ss(A_c, B_c, C_c, D_c)
N = 1/dcgain(sys_c)


sys_x = ss(A,B, eye(2),0); % the output of the system is the state
t_sim = 20
my_out = sim('ex1sim.slx')

figure
stepinfo(my_out.y.data, my_out.y.time, 1, 0,'RiseTimeLimits', [0 1], 'SettlingTimeTreshold', 0.05) 
plot(my_out.y.time, my_out.y.data);title('Transient requirements')
grid on 
