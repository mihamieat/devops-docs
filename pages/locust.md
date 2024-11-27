# install locust
```sh
pip install locust
```
# add locust file
```python
# locustfile.py
from locust import HttpUser, task

class First_Load_Test(HttpUser):
	"""Load test class."""
    @task
    def first_test(self):
		"""get root page test"""
        self.client.get("/")
```
# run locust
you then can run locust. make sure that the server to test is running
```sh
locust --headless --users 10 --spawn-rate 1 -H http://host>:<port> -t 15s --only-summary
```