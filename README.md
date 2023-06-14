# stateFeedback
#This example is Ozge Fedai's personal notes based on class examples.
M_r: reachability matrix
wn: natural frequency
t_s2: settling time 2%
S_hat : maximum overshoot
rho: final value of the step input in the simulation 

#
Only state feedback no observer no estimation 
Steps to design a successful state feedback controller:
1-Matrix definitions(A,B,C,D,x0), caution to matrix dimensions
2-Checking the reachability
  M_r: computation with ctrb(A,B)
  check if rank(A) == rank(M_r). if not equal we can not continue the state feedback controller.
  conclusion, M_r is not reachable.
3- using the formula sheet and given variables  S_hat and t_s2 or t_r, compute the zeta and the wn.
4- use wn and zeta to compute the lambda1 and lambda2
5- Lamda1 and lambda2 is required to be remembered lambda1 = -zeta*wn - j*wn*sqrt(1-zeta^2)
                                                   lambda2 = -zeta*wn + j*wn*sqrt(1-zeta^2)
6-define the modified matrices. Technically only A changed to A_c = A-BK
  find A_c in the formulary
  update A_c, B_c, C_c, D_c . 

7-define sys_c ->sys_c will be used to calculate the N
  sys_c = ss(A_c, B_c, C_c, D_c)
8-calculate the N = 1/dcgain(sys_c)
9-calculate sys_x =ss(A,B,eye(2),0)
 %%simulation %% 
 define rho  ->set this to the parameters in the step block 
        t_sim -> set this to the simulink file
10- define the out = sim("simulink_file.slx')
11- use stepinfo(out.y.data, out.y.time, 1, 0, 'RiseTimeLimits', [0 1], 'SettlingTimeTreshold', 0.05) for the requirement check
12- plot(out.y.time, out.y.data)

 
