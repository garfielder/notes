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



## Find source files
By default , an executable  records abosolute path of source files. If executable+soures are moved to a new location,   GDB cannot find the source files.

Two ways to fix: <br>
1. set substitute-path  \<src-path\>    \<dst-path\>   <br>
2. dir  \<new_directory_that_soruce_files_are_located\>   ; this adds the path into gdb source directories

## GDB init file
   * .gdbini  
      * GDB loads it during startup
   * gdb -x <init_file> # specify init file explicitly
   * gdb -ex "gdb command"
