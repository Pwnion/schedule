`schedule <https://schedule.readthedocs.io/>`__
===============================================


.. image:: https://github.com/dbader/schedule/workflows/Tests/badge.svg
        :target: https://github.com/dbader/schedule/actions?query=workflow%3ATests+branch%3Amaster

.. image:: https://coveralls.io/repos/dbader/schedule/badge.svg?branch=master
        :target: https://coveralls.io/r/dbader/schedule

.. image:: https://img.shields.io/pypi/v/schedule.svg
        :target: https://pypi.python.org/pypi/schedule

Python job scheduling for humans. Run Python functions (or any other callable) periodically using a friendly syntax.

- A simple to use API for scheduling jobs, made for humans.
- In-process scheduler for periodic jobs. No extra processes needed!
- Very lightweight and no external dependencies.
- Excellent test coverage.
- Supports scheduling async coroutines.
- Tested on Python and 3.7, 3.8, 3.9, 3.10, 3.11, 3.12

Usage
-----

.. code-block:: bash

    $ pip install git+https://github.com/Pwnion/schedule.git

.. code-block:: python

    import schedule
    import time

    def job():
        print("I'm working...")

    schedule.every(10).seconds.do(job)
    schedule.every(10).minutes.do(job)
    schedule.every().hour.do(job)
    schedule.every().day.at("10:30").do(job)
    schedule.every(5).to(10).minutes.do(job)
    schedule.every().monday.do(job)
    schedule.every().wednesday.at("13:15").do(job)
    schedule.every().day.at("12:42", "Europe/Amsterdam").do(job)
    schedule.every().minute.at(":17").do(job)

    def job_with_argument(name):
        print(f"I am {name}")

    schedule.every(10).seconds.do(job_with_argument, name="Peter")

    while True:
        schedule.run_pending()
        time.sleep(1)

.. code-block:: python

    import schedule
    import asyncio

    async def job_async():
        print("I'm working asynchronously...")
        await asyncio.sleep(5)

    schedule.every(10).seconds.do(job_async)
    schedule.every(10).minutes.do(job_async)
    schedule.every().hour.do(job_async)
    schedule.every().day.at("10:30").do(job_async)
    schedule.every(5).to(10).minutes.do(job_async)
    schedule.every().monday.do(job_async)
    schedule.every().wednesday.at("13:15").do(job_async)
    schedule.every().day.at("12:42", "Europe/Amsterdam").do(job_async)
    schedule.every().minute.at(":17").do(job_async)

    async def job_with_argument_async(name):
        print(f"I am {name}")
        await asyncio.sleep(5)

    schedule.every(10).seconds.do(job_with_argument_async, name="Peter")

    async def execute():
        while True:
            await schedule.run_pending_async()
            await asyncio.sleep(1)

    asyncio.run(execute())

Documentation
-------------

Schedule's documentation lives at `schedule.readthedocs.io <https://schedule.readthedocs.io/>`_.


Meta
----

Daniel Bader - `@dbader_org <https://twitter.com/dbader_org>`_ - mail@dbader.org

Inspired by `Adam Wiggins' <https://github.com/adamwiggins>`_ article `"Rethinking Cron" <https://adam.herokuapp.com/past/2010/4/13/rethinking_cron/>`_ and the `clockwork <https://github.com/Rykian/clockwork>`_ Ruby module.

Distributed under the MIT license. See `LICENSE.txt <https://github.com/dbader/schedule/blob/master/LICENSE.txt>`_ for more information.

https://github.com/dbader/schedule
