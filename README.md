# NU_MSDS460_KnapsackProblemDiscussion_Week5
Knapsack problem using Pythons Pulp package to optimize items we should pack for a cross country move.

#problem and values outlined below
You are moving from New Jersey to California and have rented a truck that can haul up to 1,100 cubic feet of furniture.  The volume and value of each item you are considering moving on the truck is given below. 

Which items should you take to California using the knapsack problem formulation? 
However, what unrealistic assumptions are you making about this real-life problem by using the knapsack problem? 
 

Item	Value ($)	Volume (Cubic Feet)
Bedroom set	$60	800
Dining room set	$48	600
Gaming computer	$14	300
Sofa	$31	400
TV	$10	200

#notebook text below

#import packages and variables
from pulp import *

#Create variables
bedroom_set = LpVariable("bedroom_set", 0, 1, cat = 'Integer')
dining_room_set = LpVariable("dining_room_set", 0, 1, cat = 'Integer')
computer = LpVariable("computer", 0, 1, cat = 'Integer')
sofa = LpVariable("sofa", 0, 1, cat = 'Integer')
tv = LpVariable("tv", 0, 1, cat = 'Integer')

#create problem to maximize
prob = LpProblem("problem", LpMaximize)

#define our constraints
#constraints
prob += 800*bedroom_set + 600*dining_room_set + 300*computer + 400*sofa + 200*tv <= 1100

#objective function
prob += 60*bedroom_set + 48*dining_room_set + 14*computer + 31*sofa + 10*tv 

#solve
solution = prob.solve()
#Type
LpStatus[solution]
'Optimal'

#Decision Type
for var in prob.variables():
    print(f"{var.name} = {var.varValue}")
bedroom_set = 0.0
computer = 0.0
dining_room_set = 1.0
sofa = 1.0
tv = 0.0
#results are binary. 0 = leave, 1 = pack

#value
value(prob.objective)
79.0 #our answer for optimal value of items
