General information about the CTL course available at https://ctl.polyphys.mat.ethz.ch/

# :wave: Ideal gas

The goal of this project is to write an algorithm to simulate an (ideal) gas inside a cubic box with hard walls. An ideal gas is a theoretical gas composed of many randomly moving point particles that are not subject to interparticle interactions. In the following figure, points are represented by colored spheres to make them visible and distinguishable, while ideal gas molecules are indistinguishable. 

<img src="https://www.complexfluids.ethz.ch/images/PROJECT-ideal-gas.png" width=30%>

The ideal gas model relies upon the following main assumptions:
-	The particles which compose the gas are indistinguishable, small, point-like spheres
-	The average distance between particles is much larger than the size of the particles
-	The particles are constantly moving in random directions (each individual particle is moving on a straight line until its next collition with the wall) and their speeds are distributed according to a Maxwell-Boltzmann speed distribution
-	An ideal gas obeys Newton’s laws
-	There are no attractive or repulsive forces between the particles
-	The only forces between the gas particles and the surroundings are those that determine the point-like, elastic collisions of the molecules with the walls

To write an algorithm which simulates such a gas, we suggest that you take the following steps. Note, that the steps should be distributed over python functions, to give a structure to your code. 

## Part I – Mandatory

###	1. Initial conditions

You should start by setting up the constants and the initial conditions of your simulation. More particularly this entails setting up the boundaries of your box and setting up $N$ point-like particles randomly placed inside these boundaries with their corresponding initial velocities (*Think about the fact that these initial velocities should be distributed according to a Gaussian (normal) distribution with a standard deviation of* $\sqrt{k_{\rm B}T/m}$ *where* $T$ *is the temperature of the gas and* $m$ *is the mass of one particle*).


###	2. Evolving the system in time

Once you have set up the initial conditions of your simulation you need to evolve the system over a short period of time. Simulating the evolution of a continuous dynamic system requires to choose the size of a time step and the number of steps. The time step sets the interval with which you recalculate the position of each particle. The size of the time step will vary depending on the velocity of your gas and and the size of your box. The smaller the box, the smaller the time step, and the higher the velocity, the smaller the time step, depending on your implementation. If you choose a time step that is too small, your particles will barely move inside the box while if the time step chosen is too large their positions will change too much from one time step to the next and they will appear to “jump” through the box instead of moving smoothly.

The position of each particle needs to be recalculated at each time step. There are several ways to do this but keep in mind that some are more time efficient than others (*As a general rule of thumb when programming in Python, try to avoid for loops as much as possible!*).

###	3. Including collisions with the walls

Once you have set up a way to recalculate the positions of the particles for various time steps you should include the potential collisions of the particles with the walls of the box into your simulation. Again, there are multiple ways to check which particles collide with the walls at each time step but remember to avoid for loops as much as possible.

We assume the collisions between the particles and the walls are elastic collisions, which means that the total kinetic energy before and after the collision must be conserved. Think of what this implies for the velocity vector of a particle which collides with the walls of the box.

### 4. Visualization
The simulation of the ideal gas can be visualized by plotting it in 3D with the Python library Matplotlib. To do so, you can follow the following example of how to create a 3-dimensional scatter plot: https://matplotlib.org/stable/gallery/mplot3d/scatter3d.html.

For a more elaborate visualization, look up how you can make a video with the different timesteps of your simulation to see the particles move inside the box.

### 5.	Energy conservation and momentum transfer
Compute the total experimental kinetic energy of the system at the beginning of the simulation and check whether it is properly conserved at the end of the simulation.

When a particle collides with a wall of the box, it gets rebound and transfers an amount of momentum to the wall (although the wall stays in place, it can be considered to have infinite mass) which is equal to the length of the vector difference between the particle's momentum vector before the collision and the particle's momentum vector after the collision. Compute the accumulated total momentum amount transferred to the walls at each time step and plot it as a function of time.

## Part II - Optional (Bounce-back gates)

<img src="https://www.complexfluids.ethz.ch/images/PROJECT-ideal-gas-gates.png" width="50%">

Set up two square (two-dimensional) boxes of size L *x* L (side by side on the x-axis, see figure), connected by a horizontal rectangular channel with length L and width w << L. Particles can now leave a box through the channel, and reach the other box. Particles get reflected by channel walls in the usual (elastic) manner. The rectangular channel has two parts of identical length L/2, denoted as left and right gate (see figure). Implement two additional rules: 
1. If there are more than Q particles in the left gate moving towards the right gate (= exhibiting positive x-component of the velocity), reverse the x-component of all the Q velocities (in the figure, Q=2, and the red velocities are the new velocities after velocity reversal).   
2. If there are more than Q particles in the right gate moving towards the left gate (= exhibiting negative x-component of the velocity), reverse the x-component of all the Q velocities. 

Simulate this system with N=300 particles, L=1, w=0.05. Choose random initial velocities and random initial positions inside the channel-connected array. Plot the number of particles in the left box versus time, for various integer-valued Q. There is a critical Q value beyond which one of the boxes is predominantly empty. 
