# whi_move_base
Provides an implementation of an action that, given an interaction state, will attempt to reach the target without being interrupted by other goals

## Dependency
In order to handle bypassing goals that are requested during interaction process, whi_move_base relies on the interaction type in MoveBaseGoal message. There defined [five interaction types](https://github.com/xinjuezou-whi/whi_move_base_msgs)

Clone the whi_move_base_msgs first:
```
git clone https://github.com/xinjuezou-whi/whi_move_base_msgs.git
```

## Client request
Following are snippets of client goal request, for an example:
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
Refer to belowing SM logic for further extended functions:

![move_base_state_machine drawio](https://github.com/xinjuezou-whi/whi_move_base/assets/72239958/7079ac98-8f3f-4666-a18c-3f492a1de061)
