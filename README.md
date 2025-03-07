import pandas as pd
import statsmodels.api as sm

# Define the file path
file_path = r"C:\Python files\advertising_dataset.xlsx"
df = pd.read_excel(file_path)

X = df[['digital_advertising', 'traditional_advertising']]
Y = df['return_advertising_campaign']

X = sm.add_constant(X)

model = sm.OLS(Y, X).fit()

# Display the summary
print(model.summary())

from ortools.linear_solver import pywraplp

solver = pywraplp.Solver.CreateSolver('GLOP')

# max and min budget from excel
x = solver.NumVar(0, 1, 'x')
y = solver.NumVar(0, 2, 'y')

print('Number of Variables =', solver.NumVariables())

ct = solver.Constraint(0, 2, 'ct')
ct.SetCoefficient(x, 1)
ct.SetCoefficient(y, 1)

objective = solver.Objective()
objective.SetCoefficient(x, 3)
objective.SetCoefficient(y, 1)
objective.SetMaximization()

solver.Solve()
print('Solution:')
print('Objective value =', objective.Value())
print('x =', x.solution_value())
print('y =', y.solution_value())
