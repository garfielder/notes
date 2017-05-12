# GDB 

## use GDB server to debug program remotely 

Suppose:  <br>
host server ip:  lyq_host_server<br>
remote PC that program runs on :   target_pc<br>

__*On Remote PC*__ :  <br>
gdbserver lyq_host_server:1234  my_progogram_executable <other args>; <br>

lyq_host_server is the host server that will connect to current pc <br>
1234  the listening port on current target pc <br>

__*On Host server*__:  <br>
1. Open GDB or DDD, in command windows type following commands
2. target remote <target_pc>:1234





