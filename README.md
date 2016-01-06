# codemap
Codemap is IDA plugin for run trace visualization which can be very helpful for reversing a complex software.

Imagine you are about to reverse-engineer the IE's javascript engine from scratch.
with a brief research, you will notice that the javascript engine for IE is jscript9.dll

so you open up that dll with IDA, and there are over 16 thousand complex functions.
given that most of the programs are based on OOP(Object Oriented Programming) you cannot
simply follow all the functions from the starting point(main function) and there is no main 
entry point in modules such as DLL. it is virtually impossible to understand codes and their 
relationship inside the huge DLL by just statically analyzing them.

you probably want to narrow down the codes that are actually involved to your input script.
so, you try to run the IE with sample script file and analyze it dynamically by debugging it.
but you soon realize that you don't know where to set breakpoint among 16 thousand functions.

it would take huge amount of time and effort to find the codes of your interest.
if you are not patient, you will probably just give up.

Luckily, you have a tool named Codemap.

Unlike DBI(Dynamic Binary Instrumentation) based tools such as Intel PIN or QEMU, 
Codemap only uses 'breakpoints' for tracing the program.
If program hits a breakpoint, the Codemap breakpoint handler is invoked as a callback function
then proper action for tracing is taken then Codemap continues the program.

The breakpoint event is sent to Codemap server side. The Codemap server saves this information inside Database
and plot the event for graph generation. 
Codemap uses Dygraph (Javascript based visualization tool) to plot all the breakpoint events.

Codemap has following features.
- runtrace visualization.
	Codemap generates graphical representation of execution trace 
	which can be useful to understand the program.

- module breakpoint
	Most of the commercial softwares are consisted with multiple modules(.dll or .so) 
	core functionality resides inside the same module.
	In order to trace functions inside a specific module, Codemap supports setting breakpoints to 
	all functions inside the selected module with a single click.

- function breakpoint
	In order to trace a specific function, Codemap supports setting breakpoints to
	all instructions inside a selected function with a single click.

- flexible memory pattern searching
	This is the key feature of Codemap. For instance, you can search the input data pattern from the
	Codemap run trace memory dump and easily find out which function is responsible for parsing your data.
	As Codemap saves all the tracing logs into database, you can filter / manipulate the runtrace result 
	using the SQL. This makes the tracing result suit to your interest.
	From the Codemap broser screen, search the memory pattern by typing the hex string
	or input the SQL statement to filter the trace result in your detailed favor.

- IDA static windows integration
	When you debug a program with IDA, you can't see the analyzed functions as good as 
	when you open up the single specific module with IDA for static analysis window.
	Normally, you have to recalculate the runtime EIP value into address that you can follow in IDA static window.
	To ease this with Codemap, you can just click the graph or navigate the graph with keyboard
	then, the statically analyzed IDA window(which is nice to see the codes) will automatically follow your runtime EIP. 

After processing legal stuff and fixing minor bugs, the first stable version of Codemap
will be disclosed to public via GITHUB as opensource software.
cheers!

- daehee
