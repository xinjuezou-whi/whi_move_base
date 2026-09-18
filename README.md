# whi_move_base
Provides an implementation of an action that, given an interaction state, will attempt to reach the target without being interrupted by other goals

## Dependency
To handle bypassing goals requested during the interaction, whi_move_base relies on the interaction type in the MoveBaseGoal message. Refer to the [defined interaction types](https://github.com/xinjuezou-whi/whi_move_base_msgs)

Clone the whi_move_base_msgs first:
```
git clone https://github.com/xinjuezou-whi/whi_move_base_msgs.git
```

## Client request
Following are snippets of client goal request, for example:
```
move_base_msgs::MoveBaseGoal goalMsg;
goalMsg.target_pose.header.frame_id = "map";
goalMsg.target_pose.header.stamp = ros::Time::now();
if (Goal) // Goal is a point of geometry_msgs::Pose
{
    goalMsg.target_pose.pose = *Goal;
    goalMsg.inter_type = Block ? move_base_msgs::MoveBaseGoal::INTERACTION_BLOCK :
        move_base_msgs::MoveBaseGoal::INTERACTION_UNBLOCK;
}
else
{
    goalMsg.inter_type = Block ? move_base_msgs::MoveBaseGoal::INTERACTION_BLOCK_ONLY :
        move_base_msgs::MoveBaseGoal::INTERACTION_UNBLOCK_ONLY;
}
```

## State machine
Refer to the SM logic below for further extended functions:

<img width="1048" height="899" alt="move_base_state_machine drawio" src="https://github.com/user-attachments/assets/afed1f92-d1f0-4e51-b7da-326b887270b6" />

## Extra params

```
rc_state_topic: whi_rc_bridge/rc_state
align_pattern: true
registration_action: pose_registration
registration_max_try: 3
path_block_check_distance: 0.8
path_block_check_resolution: 0.05 
path_clear_confirm_time: 0.8
pause_while_blocked: true
```
