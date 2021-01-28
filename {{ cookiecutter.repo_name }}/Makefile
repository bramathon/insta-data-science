.PHONY: clean
#################################################################################
# GLOBALS                                                                       #
#################################################################################

PROJECT_DIR := $(shell dirname $(realpath $(lastword $(MAKEFILE_LIST))))
BUCKET = {{ cookiecutter.s3_bucket }}
PROFILE = {{ cookiecutter.aws_profile }}
PROJECT_NAME = {{ cookiecutter.repo_name }}

CONDA_ROOT=$(shell conda info --base)
MY_ENV_DIR=$(CONDA_ROOT)/envs/$(ENV_NAME)

#################################################################################
# COMMANDS                                                                      #
#################################################################################

## Set up python interpreter environment and produce an environment.lock with exact package versions
environment.lock: environment.yml
ifneq ("$(wildcard $(MY_ENV_DIR))","") # check if the directory is there
	conda env update $(PROJECT_NAME) --file environment.yml --prune
else
	conda env create -f environment.yml
endif
	@echo ">>> Conda env $(PROJECT_NAME) ready. Activate with 'conda activate $(PROJECT_NAME)'"
	conda list --explicit > environment.lock

## Test python environment is set-up correctly
test_environment:
ifneq (${CONDA_DEFAULT_ENV}, $(PROJECT_NAME))
	$(error Must activate `$(PROJECT_NAME)` environment before proceeding)
endif

## Build Jupyter Lab
jupyter: test_environment
	$(MY_ENV_DIR)/bin/jupyter labextension install @jupyter-widgets/jupyterlab-manager
	$(MY_ENV_DIR)/bin/jupyter labextension install jupyterlab-plotly
	$(MY_ENV_DIR)/bin/jupyter labextension install plotlywidget
	$(MY_ENV_DIR)/bin/jupyter labextension install jupyterlab-theme-solarized-dark
	$(MY_ENV_DIR)/bin/jupyter lab build --name "$(PROJECT_NAME)"

## Lint using black
lint:
	black --verbose --target-version py38 .

# Run the unit tests
test:
	python -m unittest test.basic_tests

## Delete all compiled Python files, clean up stopped containers
clean:
	find . -type f -name "*.py[co]" -delete
	find . -type d -name "__pycache__" -delete

#################################################################################
# Self Documenting Commands                                                     #
#################################################################################

.DEFAULT_GOAL := help

# Inspired by <http://marmelab.com/blog/2016/02/29/auto-documented-makefile.html>
# sed script explained:
# /^##/:
# 	* save line in hold space
# 	* purge line
# 	* Loop:
# 		* append newline + line to hold space
# 		* go to next line
# 		* if line starts with doc comment, strip comment character off and loop
# 	* remove target prerequisites
# 	* append hold space (+ newline) to line
# 	* replace newline plus comments by `---`
# 	* print line
# Separate expressions are necessary because labels cannot be delimited by
# semicolon; see <http://stackoverflow.com/a/11799865/1968>
.PHONY: help
help:
	@echo "$$(tput bold)Available rules:$$(tput sgr0)"
	@echo
	@sed -n -e "/^## / { \
		h; \
		s/.*//; \
		:doc" \
		-e "H; \
		n; \
		s/^## //; \
		t doc" \
		-e "s/:.*//; \
		G; \
		s/\\n## /---/; \
		s/\\n/ /g; \
		p; \
	}" ${MAKEFILE_LIST} \
	| LC_ALL='C' sort --ignore-case \
	| awk -F '---' \
		-v ncol=$$(tput cols) \
		-v indent=19 \
		-v col_on="$$(tput setaf 6)" \
		-v col_off="$$(tput sgr0)" \
	'{ \
		printf "%s%*s%s ", col_on, -indent, $$1, col_off; \
		n = split($$2, words, " "); \
		line_length = ncol - indent; \
		for (i = 1; i <= n; i++) { \
			line_length -= length(words[i]) + 1; \
			if (line_length <= 0) { \
				line_length = ncol - indent - length(words[i]) - 1; \
				printf "\n%*s ", -indent, " "; \
			} \
			printf "%s ", words[i]; \
		} \
		printf "\n"; \
	}' \
	| more $(shell test $(shell uname) = Darwin && echo '--no-init --raw-control-chars')
