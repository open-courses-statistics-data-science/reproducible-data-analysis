```R
library(deSolve)

simulate_SIR <- function(S0, I0, R0, Tstart, Tf, timestep, gamma, beta, N, method="lsoda", atol=1e-6, rtol=1e-06)
  {
      dxdt <- function(t, y, parms) {
	  list(
	      derivatives=c(
		  dSdt=-beta*y[1]*y[2]/N,
		  dIdt=beta*y[1]*y[2]/N - gamma*y[2],
		  dRdt=gamma*y[2]
	      )
	  )
      }

      times <- seq(from = 0, to = Tf, by = timestep)
	  parms <- c(beta=beta, gamma=gamma, N=N)
      ode(c(S0, I0, 0), times, dxdt, parms, method, atol, rtol)
  }
```

