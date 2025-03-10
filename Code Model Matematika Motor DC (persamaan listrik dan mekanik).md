//Nama : Andi Muhammad Fadhli
//NIM : 235150301111036

import sympy as sp

# Define symbols
L, R, V, K, theta, I, doti, J, b, s, t, omega, omegadot = sp.symbols('L, R, V, K, \\theta, I, \\dot{i}, J, b, s, t, omega,\\dot{\\omega}')

dIdt = (sp.Function('I')(t).diff(t))
dthetadt = (sp.Function('\\theta')(t).diff(t))
#display(dIdt)

#eq1 = L *dIdt + R * I - V + K * dthetadt  # Electrical equation
#eq2 = J * dthetadt**2 + b * dthetadt + K * I  # Mechanical equation

eq1 = L *doti + R * I - V + K * omega  # Electrical equation
eq2 = J * omegadot + b * omega + K * I  # Mechanical equation

display(eq1)
display(eq2)
