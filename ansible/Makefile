.PHONY : help

define _printhelp
	@echo '--------------------------------------------------'; \
	echo '  $(1) tools'; \
	echo '--------------------------------------------------'; \
	grep -hE '^[a-zA-Z_-]+:.*?## \[.*$(1).*\] .*$$' $(MAKEFILE_LIST) | sed -E 's/ \[.*$(1).*\]//g' |awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m: %s\n", $$1, $$2}'
endef

ifeq ($(ANSIBLE_LOG_PATH),)
	ANSIBLE_LOG_PATH = logs/ansible-$$(date +%Y%m%d-%H%M%S).log
endif

define _run_Playbook
	@ANSIBLE_LOG_PATH=$(ANSIBLE_LOG_PATH) \
	ansible-playbook -i hosts $(1) $(ANSIBLE_EXTRA_OPTIONS)
endef

help: ## [common] show list
	@$(call _printhelp,common)
	@$(call _printhelp,install)
#	@$(call _printhelp,maintenance)
#	@$(call _printhelp,develop)

install: check-connection ## [install] setup server
	@$(call _run_Playbook,playbook_install.yml,)

check-connection: ## [install,maintenance] check connection
	@$(call _run_Playbook,install/playbook_check_connection.yml,)
