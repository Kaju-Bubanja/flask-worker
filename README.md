# Flask-Worker

Flask-Worker simplifies interaction with a Redis Queue for executing long-running tasks in a Flask application. 

Long-running tasks are managed by a Worker, who sends the client a loading page until it completes the task. Upon completing the task, the Worker automatically replaces the client's window with the loaded page.

## Example

Suppose a model (the employer) must run a long, complex task before the next page loads.

What we want is for the complex task to run once, and for the view function to return a loading page while the complex task is running. Additional requests to this route should not cause the complex task to run multiple times. Once the task is complete, the loaded page should appear automatically. We can achieve this with the following:

```python
@app.route('/example1')
def example1():
    print('Request for /example1')
    employer = get_model(Employer, 'employer1')
    worker = employer.worker
    if not worker.job_finished:
        return worker()
    return 'Example 1 finished'
```

## Documentation

You can find the latest documentation at [https://dsbowen.github.io/flask-worker](https://dsbowen.github.io/flask-worker).

## License

Publications which use this software should include the following citations for Flask-Worker and its dependency, [SQLAlchemy-Mutable](https://pypi.org/project/sqlalchemy-mutable/).

Bowen, D.S. (2019). Flask-Worker [Compluter software]. [https://github.com/dsbowen/flask-worker](https://github.com/dsbowen/flask-worker)

Bowen, D.S. (2019). SQLAlchemy-Mutable [Computer software]. [https://github.com/dsbowen/sqlalchemy-mutable](https://github.com/dsbowen/sqlalchemy-mutable)

This project is licensed under the MIT License [LICENSE](https://github.com/dsbowen/flask-worker/blob/master/LICENSE).