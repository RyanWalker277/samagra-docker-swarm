# Extract the service and stack names from the target
service := $(patsubst redeploy-%, %, $(filter redeploy-%, $(MAKECMDGOALS)))
stack := $(word 2, $(MAKECMDGOALS))

ifeq ($(service),)
ifeq ($(firstword $(MAKECMDGOALS)),remove)
stack := $(word 2, $(MAKECMDGOALS))
else
$(error Please provide a service name. Usage: make redeploy-<service-name> <stack-name>)
endif
endif

redeploy: redeploy-$(service)

redeploy-%:
ifeq ($(stack),)
	$(error Please provide a stack name. Usage: make redeploy-<service-name> <stack-name>)
else
	docker stack deploy -c <(docker-compose -f docker-compose-$*.yml config) $(stack)
endif

remove:
ifeq ($(stack),)
	$(error Please provide a stack name. Usage: make remove <stack-name>)
else
	docker stack rm $(stack)
endif