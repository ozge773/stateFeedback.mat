State Feedback

This example is Ozge Fedai's personal notes based on class examples.
Variables

    M_r: Reachability matrix
    wn: Natural frequency
    t_s2: Settling time 2%
    S_hat: Maximum overshoot
    rho: Final value of the step input in the simulation

Steps to Design a Successful State Feedback Controller:

    Matrix Definitions (A, B, C, D, x0)
        Caution: Pay attention to matrix dimensions.

    Checking the Reachability
        Compute M_r using ctrb(A, B).
        Check if rank(A) is equal to rank(M_r). If they are not equal, it is not possible to continue with the state feedback controller.
        Conclusion: M_r is not reachable.

    Computing zeta and wn
        Use the formula sheet and given variables S_hat and t_s2 (or t_r) to compute zeta and wn.

    Computing lambda1 and lambda2
        Use wn and zeta to compute lambda1 and lambda2.
        Remember: lambda1 = -zeta * wn - j * wn * sqrt(1 - zeta^2)
        lambda2 = -zeta * wn + j * wn * sqrt(1 - zeta^2)

    Define the Modified Matrices
        Only A is changed to A_c = A - BK.
        Find A_c in the formula sheet.
        Update A_c, B_c, C_c, D_c.

    Define sys_c
        sys_c will be used to calculate N.
        sys_c = ss(A_c, B_c, C_c, D_c).

    Calculate N
        N = 1 / dcgain(sys_c).

    Calculate sys_x
        sys_x = ss(A, B, eye(2), 0).

    Simulation Setup
        Define rho: Set this to the parameters in the step block.
        Define t_sim: Set this to the simulink file.

    Simulation
        Define out = sim("simulink_file.slx").

    Requirement Check
        Use stepinfo(out.y.data, out.y.time, 1, 0, 'RiseTimeLimits', [0 1], 'SettlingTimeTreshold', 0.05) for the requirement check.

    Plotting
        Plot out.y.time against out.y.data.
 
