
ifdef Participants
SEATS = $(Participants)
else
SEATS = 5
endif

.PHONY: clean doc


clab: pinglab.clab.yml
	sudo ip link add lan type bridge
	sudo ip link set dev lan up
	sudo clab deploy


clean:
	-sudo clab destroy -c
	-sudo ip link delete lan
