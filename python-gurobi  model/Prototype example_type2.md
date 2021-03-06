
# Prototype example
*POLab*
<br>
*2017/10/08*
<br>
[【回到首頁】](https://github.com/PO-LAB/Python-Gurobi)

### ● 題目<br>
<img src="https://github.com/wurmen/Gurobi-Python/blob/master/python-gurobi%20%20model/picture/Prototype%20example%20picture/Prototype%20example%E9%A1%8C%E7%9B%AE.png" width="500">
<br>

### ● 數學式轉換<br>
<img src="https://github.com/wurmen/Gurobi-Python/blob/master/python-gurobi%20%20model/picture/Prototype%20example%20picture/Prototype%20example_type2%E7%AC%A6%E8%99%9F%E8%A8%AD%E5%AE%9A.png" width="350">
<br>
<img src="https://github.com/wurmen/Gurobi-Python/blob/master/python-gurobi%20%20model/picture/Prototype%20example%20picture/Prototype%20example_type2_%E6%95%B8%E5%AD%B8%E5%BC%8F%E8%BD%89%E6%8F%9B.png" width="650">
<br>




## Import gurobipy


```python
from gurobipy import*
```

## Model


```python
    m=Model('Protorype example_type2')
```

## Add parameters

```python
    I=2
    J=3
    v=[3,5]
    p=[[1,0,3],[0,2,2]]
    a=[4,12,18]
```

## Add decision variables


```python
    x={}
    for i in range(I):
        x[i]=m.addVar(lb=0,vtype=GRB.CONTINUOUS,name='x_%d'%i)
```

## Update


```python
    m.update()
```

## Add objective and constraints
<img src="https://github.com/wurmen/Gurobi-Python/blob/master/python-gurobi%20%20model/picture/Prototype%20example%20picture/Prototype%20example_type2_S.png" width="400">

```python
    m.setObjective(quicksum(v[i]*x[i] for i in range(I)),GRB.MAXIMIZE)
    
    for j in range(J):
        m.addConstr(quicksum(p[i][j]*x[i] for i in range(I))<=a[j],name='c0')
```

## Result


```python
    m.optimize()
    print('obj:%d'%m.objVal)
    for v in m.getVars():
        print('%s:%d'%(v.varName,v.x))
```

    Optimize a model with 3 rows, 2 columns and 4 nonzeros
    Coefficient statistics:
      Matrix range     [1e+00, 3e+00]
      Objective range  [3e+00, 5e+00]
      Bounds range     [0e+00, 0e+00]
      RHS range        [4e+00, 2e+01]
    Presolve removed 2 rows and 0 columns
    Presolve time: 0.13s
    Presolved: 1 rows, 2 columns, 2 nonzeros
    
    Iteration    Objective       Primal Inf.    Dual Inf.      Time
           0    4.2000000e+01   1.500000e+00   0.000000e+00      0s
           1    3.6000000e+01   0.000000e+00   0.000000e+00      0s
    
    Solved in 1 iterations and 0.15 seconds
    Optimal objective  3.600000000e+01
    obj:36
    x_0:2
    x_1:6
    
