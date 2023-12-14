# -s means silent mode
# The command executed along with the output will be displayed on the terminal
# To get only the ouput use 'silent' mode
#
# make target -s


# -n or --just-print 
# The first test I perform on a new makefile target is to invoke make with the --just-print (-n) option. 
# This causes make to read the makefile and print every command it would normally execute to 
# update the target but without executing them.
#
# make target -n


# When you run make with the -i or --ignore-errors flag, 
# errors are ignored in all recipes of all rules. 
# A rule in the makefile for the special target .IGNORE has the same effect, 
# if there are no prerequisites. This is less flexible but sometimes useful.
# When errors are to be ignored, because of -i flag, make treats an error return just like success,
# except that it prints out a message that tells you the status code the shell exited with, 
# and says that the error has been ignored.
#
# make target -i 


.IGNORE:
	compile
	simulate

# WE can also use the target where we WANT the silent mode 
.SILENT:
	compile
	simulate

# For Assertions use +acc options
#  +cover=becstf
compile:
	vlib work; 
	vlog -sv \
	+acc \
	+cover \
	+fcover \
	-l compile.log \
	-f .svunit.f 

simulate:
	# Use -novopt for no optimization - Makes the simulation slower
	# vsim -pli finesim.so -coverage top
	vsim -vopt \
	work.testrunner \
	-voptargs=+acc=npr \
	-assertdebug \
	-l run.log \
	-sva \
  -coverage \
	-c -do "log -r /*; add wave -r /*; run -all; exit" \
	-wlf waveform.wlf

	# To open the waveform use the below command 
	# vsim -view waveform.wlf &
	#
	# To open the wavefrom with saved signals
	# vsim -view waveform.wlf -do i3c_waves.do &

clean_simulate:
	rm -rf *_test*

clean_compile:
	rm -rf work/ *_compile.log transcript waveform.wlf

clean:
	make clean_compile

all: 
	make clean
	make compile
	make simulate
