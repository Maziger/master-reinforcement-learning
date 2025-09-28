# 7.8.2 Exercise - Car rental

Consider a rental company with two locations, each with a capacity of 20 cars. Each day, customers arrive at each location to rent cars. If a car is available, it is rented out with a reward of $10. Otherwise the opportunity is lost. Cars become available for renting the day after they are returned.

The number of cars rental requests D_i at Location i = 1,2 are Poisson distributed with mean 3 and 4. Similar, the number of cars returned H_i at Location i = 1,2
are Poisson distributed with mean 3 and 2. Cars returned resulting in more cars than the capacity are lost (and thus disappear from the problem).

To ensure that cars are available where they are needed, they can be moved between the two locations overnight, at a cost of $2 per car. A maximum of five cars can be moved from one location to the other in one night.

Formulate the problem as an finite MDP where the time-steps are days.

1. Define the state space (with states(x,y)) equal the number of cars at each location at the end of the day.

s = {(x,y)|0 <= x <= 20, 0 <= y <= 20} 

Both rental locations have a capacity of 20 cars.

2. Define the action space equal the net numbers of cars moved from Location 1 to Location 2 overnight, i.e. negative if move from Location 2 to 1.

Action a = net cars moved from Location 1 to Location 2: 
Range: a {-5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5}
Meaning:
  a > 0: move a cars from location 1 to 2
  a < 0: move a cars from location 2 to 1
  a = 0: no movement



A(s) = {a | -min(5, y, 20 - x) <= a <= min(5, x, 20 - y)}
Meaning: 
  Maximum 5 cars can be moved in either direction
  Can't move more cast than availlable at the source location (x,y)
  Can't exceed the capacity of 20 at the destination location

3. Calculate the expected reward r(s,a)
???...???



4. Give the inventory dynamics for Location 2
Note the inventory dynamics (number of cars) at each parking lot is independent of the other given an action a. Let us consider Location 1 and assume that we are in state x and chose action a. Then the number of cars after movement is x - a and after rental requests x - a - min(D_1, x - a). Next, the number of retured cars are added:
x - a - min(D_1, x - a) + H_1. Finally, note that if this number is above 20 (parking lot capacity), then we only have 20 cars, i.e. the inventory dynamics (number of cars at the end of the day) is:
   X = min(20, x - a - min(D_1, x - a) + H_1))

Inventory dynamics for location 2 (opposite of location 1): 
  Y = min(20, y + a - min(D_2, y + a) + H_2))
