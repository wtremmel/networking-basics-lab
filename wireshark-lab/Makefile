
ifdef Participants
SEATS = $(Participants)
else
SEATS = 5
endif

.PHONY: doc clean

docker-compose.yml: create-docker-compose
	./create-docker-compose -n $(SEATS) > docker-compose.yml

# doc:
# 	$(MAKE) -C doc

clean:
	-docker compose down
	-rm -rf config
	-rm docker-compose.yml
# 	-$(MAKE) -C doc clean

