# An SIR simulation

```{#initcode data-line-numbers="|3"}
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

# The population size doesn't have to be passed {data-auto-animate=""}

```{.R .numberLines data-id="redundant-param" data-line-numbers="3"}
  library(deSolve)

  simulate_SIR <- function(N, S0, I0, R0, Tstart, Tf, timestep, gamma, beta, method="lsoda", atol=1e-6, rtol=1e-06)
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

# The population size doesn't have to be passed {data-auto-animate=""}

```{.R .numberLines data-id="redundant-param" data-line-numbers="5"}
  library(deSolve)

  simulate_SIR <- function(S0, I0, R0, Tstart, Tf, timestep, gamma, beta, method="lsoda", atol=1e-6, rtol=1e-06)
  {
      N <- S0 + I0 + R0
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

# Grouping parameters that travel together {data-auto-animate=""}

```{.R .numberLines data-id="group-parameters" data-line-numbers="1"}
simulate_SIR <- function(S0, I0, R0, Tstart, Tf, timestep, gamma, beta, method="lsoda", atol=1e-6, rtol=1e-06)
  {
    N <- S0 + I0 + R0
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

# Grouping parameters that travel together {data-auto-animate=""}

```{.R .numberLines data-id="group-parameters" data-line-numbers="1|13|14,15"}
simulate_SIR <- function(init_state, model_parms, solver_parms, Tstart, Tf)
{
  dxdt <- function(t, y, parms) {
	list(
	    derivatives=c(
		dSdt=-parms$beta*y[1]*y[2]/parms$N,
		dIdt=parms$beta*y[1]*y[2]/parms$N - parms$gamma*y[2],
		dRdt=parms$gamma*y[2]
	    )
	)
  }

  times <- seq(from = Tstar, to = Tf, by = model_parms$timestep)
  parms <- c(model_parms, N=sum(init_state))
  ode(init_state, times, dxdt, parms, solver_parms$method, solver_parms$atol, solver_parms$rtol)
}
```

# A common pattern for all variable names {data-auto-animate=""}

```{.R .numberLines data-id="naming-pattern" data-line-numbers="1,13|6,7"}
simulate_SIR <- function(init_state, model_parms, solver_parms, Tstart, Tf)
{
  dxdt <- function(t, y, parms) {
    list(
      derivatives=c(
        dSdt=-parms$beta*y[1]*y[2]/parms$N,
        dIdt=parms$beta*y[1]*y[2]/parms$N - parms$gamma*y[2],
        dRdt=parms$gamma*y[2]
	    )
     )
  }

  times <- seq(from = Tstart, to = Tf, by = model_parms$timestep)
  parms <- c(model_parms, N=sum(init_state))
  ode(init_state, times, dxdt, parms, solver_parms$method, solver_parms$atol, solver_parms$rtol)
}
```
# A common pattern for all variable names {data-auto-animate=""}

```{.R .numberLines data-id="naming-pattern" data-line-numbers="1,13|6,7"}
simulate_SIR <- function(init_state, model_parms, solver_parms, min_time, max_time)
{
  dxdt <- function(t, y, parms) {
    list(
      derivatives=c(
        dSdt=-parms$beta*y[1]*y[2]/parms$population_size,
        dIdt=parms$beta*y[1]*y[2]/parms$population_size - parms$gamma*y[2],
        dRdt=parms$gamma*y[2]
	    )
     )
  }

  times <- seq(from = min_time, to = max_time, by = model_parms$timestep)
  parms <- c(model_parms, population_size=sum(init_state))
  ode(init_state, times, dxdt, parms, solver_parms$method, solver_parms$atol, solver_parms$rtol)
}
```

#
before
```{.R .numberLines data-line-numbers=""}
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
after
```{.R .numberLines data-line-numbers=""}
simulate_SIR <- function(init_state, model_parms, solver_parms, min_time, max_time) {
  dxdt <- function(t, y, parms) {
    list(
	  derivatives = c(
	    dSdt = -parms$beta * y[1] * y[2] / parms$population_size,
	    dIdt = parms$beta * y[1] * y[2] / parms$population_size - parms$gamma * y[2],
	    dRdt = parms$gamma * y[2]
	  )
	)
  }
  times <- seq(from = min_time, to = max_time, by = model_parms$timestep)
  parms <- c(model_parms, population_size = sum(init_state))
  ode(init_state, times, dxdt, parms, solver_parms$method, solver_parms$atol, solver_parms$rtol)
}
```

# Recap

A short list of parameters make the scope of a function clearer at first glance.

- Identify parameters that travel together ("data clumps").
- Group these parameters into a common data structure (vector, list or class).
- Choose descriptive names.
- Consider splitting the function into smaller specialized functions.

# Going the extra mile: an `SIR_init_state` class

```{.R .numberLines}
print.SIR_init_state <- function(obj) {
  print("Initial state for an SIR model with:")
  print(sprintf("   S0 = %f", obj$S))
  print(sprintf("   I0 = %f", obj$I))
  print(sprintf("   R0 = %f", obj$R))
}


init_state <- list(S = 998, I = 2, R = 0)
class(init_state) <- "SIR_init_state"

print(init_state)
```



