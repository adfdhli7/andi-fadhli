import sympy as sp

# Definisi variabel simbolik
t, s = sp.symbols('t s')
V, I, L, R, Kb, J, B, T, omega = sp.symbols('V I L R Kb J B T omega')

# Model Matematis Motor DC
# Persamaan listrik: V = L (dI/dt) + R I + Kb * omega
V_eq = sp.Eq(V, L * sp.diff(I, t) + R * I + Kb * omega)

# Persamaan mekanik: J (domega/dt) + B * omega = T
T_eq = sp.Eq(J * sp.diff(omega, t) + B * omega, T)

# Hubungan Torsi: T = Kt * I
Kt = sp.Symbol('Kt')
T_subs = T_eq.subs(T, Kt * I)

# Transformasi Laplace
sI, sOmega = sp.symbols('I(s) omega(s)')
V_s = sp.symbols('V(s)')

V_eq_s = sp.Eq(V_s, L * s * sI + R * sI + Kb * sOmega)
T_eq_s = sp.Eq(J * s * sOmega + B * sOmega, Kt * sI)

# Fungsi alih hubungan omega(s) / V(s)
I_s_expr = sp.solve(V_eq_s, sI)[0]
T_s_expr = T_eq_s.subs(sI, I_s_expr)
Omega_s_expr = sp.solve(T_s_expr, sOmega)[0]
G_s = sp.simplify(Omega_s_expr / V_s)

# Menampilkan hasil
print("Model Matematis Motor DC:")
print(V_eq)
print(T_eq)
print("\nTransformasi Laplace:")
print(V_eq_s)
print(T_eq_s)
print("\nFungsi Alih Hubungan (G(s) = Omega(s) / V(s)):")
print(G_s)
