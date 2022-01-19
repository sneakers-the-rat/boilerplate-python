A [[Testing]] Framework for [[Python]]


# Setup

For a basic setup with pytest and [[Coveralls]], install 
- pytest
- pytest-cov
- coveralls

If using [[Poetry]], make them [[Poetry#Optional_Dependencies|Optional Dependencies]] like `poetry add --optional pytest pytest-cov coveralls`, and then specify them for the `tests` extra like

```toml
[tool.poetry.extras]
tests = ["pytest", "pytest-cov", "coveralls"]
```

## pytest.ini

You can set your pytest settings in `pytest.ini` rather than passing them as CLI arguments, like

```ini
[pytest]
addopts = --cov=autopilot --cov-config=.coveragerc --cov-report term-missing
```

# Project Structure

- inside a directory `tests`
- files that start with `test_`
- functions that start with `test_`

# Parameterization
- [Parameterizing Fixtures](https://docs.pytest.org/en/latest/how-to/parametrize.html)


## Using a Fixture to supply Parameters
To run a test for every result of an iterator fixture, 

```python
@pytest.fixture(scope="function", params=[1,2,3])  
def active_deployments(request):  
    value = request.param  
    yield value


def test_active_deployments(active_deployments):
    print(active_deployments)
	# 1, 2, or 3
```