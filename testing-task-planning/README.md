# Overview
A quick overview of how to test tasks.

Three things need to happen before testing task_planning in simulation:
 - run a docker container and ssh in
 - Start simulation (refer to simulation readme)
 - Run motion planning launch file

Notes:
 - If you don't want to open new ssh terminals, use `&` after your commands
 - remember to run `roscore &` before running any ros commands
 - remember to source your ros workspace in each new terminal: `source /opt/ros/kinetic/setup.bash`
 
# SSH into Docker
Refer to the Docker readme in the documentation repo for how to run the container and ssh in. Make sure to use the dukerobotics/robosub-ros:simulation image and mount the robosub-ros folder on your computer to the robosub-ros folder in the container in the run command. Also make sure to mount port 8080 in addition to port 2200 (see simulation readme).

# Start Simulation
Refer to the simulation readme for how to get the simulation running and communicating between docker and your computer. Make sure `ros_coppelia_comm.py` is printing out values.

# Run motion planning launch file
If you have not yet built your catkin workspace, run `catkin build` in the catkin_ws folder. Source the workspace by running `source devel/setup.bash` from the catkin_ws folder.

Then, run `roslaunch execute motion.launch sim:=true`. This runs the launch file `motion.launch` from the `execute` package in simulation mode. If it says the package is not found, that usually means you have not sourced your workspace. `motion.launch` starts controls, sensor_fusion, etc. Check out the file for the specifics of what it does. 

# Testing
Run tasks by running `python task_runner.py` from the scripts folder in motion-planning. Change the task being run in `competition_task.py`. Motion-planning should publish to /controls/desired_pose, which controls listens to. The simulation listens to /sim/move, which controls publishes to.
