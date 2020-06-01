from math import *
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
from google.colab import files
 
def acc(speed):  # Differentialekvationen
    return (d*g*V - m*g - np.sign(speed)*0.5*d*A*Cd*speed**2)/m
 
 
# Data pingisboll
m = 0.0027  # Massan för pingisboll
r = 0.020  # Radien för pingisboll
Cd = 0.47  # Drag koefficient för cirkulär tvärsnittsarea
ef = 0.91  # Studskoefficient
V = (4*pi*r**3)/3  # Volymen
A = pi*r**2  # Tvärsnittsarean
 
# Fysikaliska data
d = 1.2041  # Densitet för luft 20 C, 1 atm
g = 9.82  # Tyngdaccelerationen
 
# Simulationsdata
deltaT = 0.001  # Tidssteg i simulationen
T = 2.0  # Antal sekunder simulationen varar
 
 
N = int(T/deltaT)
h = 0
 
data2 = pd.DataFrame([[0, 0]], columns=['h0', 'h'])
 
for i in range(30, 300, 10):
    h0 = i/100
    h = 0
    # Begynnelsevillkor
    data = pd.DataFrame([[0, (d*g*V - m*g)/m, 0, h0]], columns=['Tid', 'Acceleration', 'Hastighet', 'Sträcka'])
 
    # Löser differentialekvationen numeriskt
    for n in range(1, N+1):
        t = round(deltaT*n, 4)
        v = data.Hastighet[n-1] + data.Acceleration[n-1]*deltaT
        s = data.Sträcka[n-1] + data.Hastighet[n-1]*deltaT
        if s < 0:
            v = -ef*v
            s = 0
        a = acc(v)
        data.loc[n] = [t, a, v, s]
        if data.Sträcka[n] < data.Sträcka[n-1] and data.Sträcka[n-2] < data.Sträcka[n-1]:
            h = data.Sträcka[n-1]
            break
    data2.loc[int(i/10-2)] = [h0, h]
 
# Plottar lösningen
data2.plot.scatter(x='h0', y='h', s=1, c='red')
plt.show()
 
data2.to_csv("BordtennisDataTeori.csv", index=False)
 
files.download("BordtennisDataTeori.csv")





Code for regression

