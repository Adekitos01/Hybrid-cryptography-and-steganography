.PHONY: tag
tag:
	@echo "Create tag"
	@git checkout main; 
	@git pull origin main; 
	@git fetch;
	@git tag -a  $(name) -m "$(name)"; 
	@git push origin $(name);
	@git push origin main

.PHONY: check
check:
	@echo "Run isort"
	@exec isort --check-only .
	@echo "Run black"
	@exec black --check --diff hybrid_rsa_aes tests
	@echo "Run flake"
	@exec flake8 hybrid_rsa_aes tests
	@echo "Run bandit"
	@exec bandit -r hybrid_rsa_aes/*
	@echo "Run mypy"
	@exec mypy hybrid_rsa_aes
	@exec rm -rf .mypy_cache
	
.PHONY: lint
lint:
	@echo "Run isort"
	@exec isort .
	@echo "Run black"
	@exec black hybrid_rsa_aes tests
	@echo "Run flake"
	@exec flake8 hybrid_rsa_aes tests
	@echo "Run bandit"
	@exec bandit -r hybrid_rsa_aes/*
	@echo "Run mypy"
	@exec mypy hybrid_rsa_aes
	@exec rm -rf .mypy_cache

.PHONY: test
test:
	@echo "Run tests"
	PYTHONPATH=${PYTHONPATH} PYTHONASYNCIODEBUG=x py.test -svvv -rs --cov hybrid_rsa_aes --cov-report term-missing -x
	@exec rm -rf .pytest_cache

.PHONY: clean
clean:
	@echo "Clear temp files"
	@rm -rf `find . -name __pycache__`
	@rm -rf `find . -type f -name '*.py[co]' `
	@rm -rf `find . -type f -name '*~' `
	@rm -rf `find . -type f -name '.*~' `
	@rm -rf `find . -type f -name '@*' `
	@rm -rf `find . -type f -name '#*#' `
	@rm -rf `find . -type f -name '*.orig' `
	@rm -rf `find . -type f -name '*.rej' `
	@rm -rf .coverage
	@rm -rf coverage.html
	@rm -rf coverage.xml
	@rm -rf htmlcov
	@rm -rf build
	@rm -rf cover
	@python setup.py clean
	@rm -rf .develop
	@rm -rf .flake
	@rm -rf .install-deps
	@rm -rf *.egg-info
	@rm -rf .pytest_cache
	@rm -rf dist

.PHONY: help
help:
	@echo -n "Common make targets"
	@echo ":"
	@cat Makefile | sed -n '/^\.PHONY: / h; /\(^\t@*echo\|^\t:\)/ {H; x; /PHONY/ s/.PHONY: \(.*\)\n.*"\(.*\)"/  make \1\t\2/p; d; x}'| sort -k2,2 |expand -t 20
