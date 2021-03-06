# simp_process_graph
This holds the tool we are using to draw the process graphs

This code allows you to plot the communications between your host and others.
It uses the lsof (list open files) command with the -i4 (using ipv4 protocol) and -n (converts hostnames to ip addresses),
creates an array of hashes of (process id, process name, port, filename, hostname, owner), 
writes the interim data to a file,
and creates a graph, boxing up where the user and process are the same, and where destinations are the same.
Lines are color-alternated to keep them distinct.

Files included

* graph_ip_process.rb - ruby code to create the plots

  note - there are 2 lines that would be most commonly commented out:
  
  Comment out for a test file (would be called i4_processes)
  
      system ("lsof -i4 -n > #{infile}")

  Conversion may not work on some versions, and may be convertable to the jpg on another system 
  (if this errors out, we still have the dot file)  
  
      exec "dot -Tjpg #{infile}.dot -o #{infile}.jpg"


* i4_processes - the command output is piped to this file
* i4_processes_sorted - the actual hashes written out
* i4_processes.dot - the dot file of the graph
* i4_processes.jpg - the jpeg picture of the graph

In order to run, you must

$yum install ruby 

$yum install 'graphviz*'

$gem install gviz

Run:
$ ruby graph_ip_process.rb

note: to test with known data, rename the i4_processes_simple or i4_processes_complex to ip_processes and comment out the line that does the lsof
